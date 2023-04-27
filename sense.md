# Hack the Box - Sense

```CSS
Machine IP: 10.10.10.60
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.60 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.60
Host is up (0.18s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 129.73 seconds
```

```CSS
▶ nmap -sC -sV -p 80,443 10.10.10.60 -oN deep.nmap

Nmap scan report for 10.10.10.60
Host is up (0.18s latency).

PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.10.10.60/
443/tcp open  ssl/http lighttpd 1.4.35
|_http-title: Login
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_http-server-header: lighttpd/1.4.35
|_ssl-date: TLS randomness does not represent time

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.14 seconds
```

---

## HTTP/ HTTPS
![image](https://user-images.githubusercontent.com/83878909/234785069-bf67c3ce-c4ee-4b1b-aec8-85854c54acc7.png)

---

## Content Discovery
  - Directory and File Brute-force
```CSS
▶ gobuster dir -u https://10.10.10.60 -w /seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --no-tls-validation -x txt -t 50
```
![image](https://user-images.githubusercontent.com/83878909/234785696-2768758a-7b87-4b57-8a49-8793f79058fc.png)

  - `https://10.10.10.60/changelog.txt`
![image](https://user-images.githubusercontent.com/83878909/234785981-a79b17a3-ffc3-4539-9daf-e04081cb0de8.png)

  - `https://10.10.10.60/system-users.txt`
![image](https://user-images.githubusercontent.com/83878909/234786961-5d7409e2-ae45-4b16-af9a-02cb3aeda529.png)

---

## PFSense
  - Login
![image](https://user-images.githubusercontent.com/83878909/234787699-4a1e1e3d-b3bc-47e2-b9c1-a0c50f013da5.png)
  
  - Dashboard
![image](https://user-images.githubusercontent.com/83878909/234787909-2f6a4e32-e1b6-42a6-b693-b50abde265dc.png)

### Searchsploit
```CSS
▶ searchsploit pfsense 2.1.3
```
![image](https://user-images.githubusercontent.com/83878909/234788791-20fa0822-ab0f-436c-9c6c-0da7410f5969.png)
![image](https://user-images.githubusercontent.com/83878909/234789403-f7e2d729-499e-4a74-bec7-70138323b219.png)

```CSS
▶ 
```
