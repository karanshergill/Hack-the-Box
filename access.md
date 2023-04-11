# Hack the Box - Access

```CSS
Machine IP: 10.10.10.98
```

- [NMAP: All TCP ports](#nmap-open-ports)
- [NMAP: Open ports Service Version](#nmap-service-version)
- [FTP Anonymous Login](#ftp-login)
  - [Download Files](#ftp-downloads)
- [Telnet Anonymous Login](#telnet-anonymous-login)
- [Website](#webserver)

## NMAP Open Ports
```CSS
▶ nmap -Pn -sS -p- 10.10.10.98 -T4 --min-rate 5000 -oN nmap.surface

Nmap scan report for 10.10.10.98
Host is up (0.19s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT   STATE SERVICE
21/tcp open  ftp
23/tcp open  telnet
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 26.68 seconds
```

## NMAP Service Version
```CSS
▶ nmap -sC -sV -p 21,23,80 10.10.10.98 -T4 --min-rate 5000 -oN nmap.deep

Nmap scan report for 10.10.10.98
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 425 Cannot open data connection.
23/tcp open  telnet?
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-title: MegaCorp
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 187.59 seconds
```

## FTP Login
  - Log in to ftp, anonymous login allowed. 
```CSS
▶ ftp 10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/231272883-d87603cc-e9b5-461c-a670-5c36226f6a57.png)

### FTP Downloads
  - Download all directories and files found in FTP.
```CSS
▶ wget -m --no-passive ftp://anonymous:anonymous@10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/231274006-305f40e6-8efc-4af0-8f4c-6e85319bab51.png)



---

## Telnet Anonymous Login
  - Telent log in failed.
```CSS
▶ telnet 10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/231275176-f81e52d6-3975-497a-b375-17f4cc9eb3e2.png)

---

## Website
![image](https://user-images.githubusercontent.com/83878909/231276321-d9810c39-9ac9-4c59-b50d-0f7a296ede38.png)

---
