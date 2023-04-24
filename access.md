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

---

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

### ZIP File
  - Access File
```CSS
▶ 7z x Access\ Control.zip
```
![image](https://user-images.githubusercontent.com/83878909/233909981-8b6ad107-b1cf-4ad8-87f8-fc00f663bc5b.png)

  - Technical Information
```CSS
▶ 7z l -slt Access\ Control.zip
```
![image](https://user-images.githubusercontent.com/83878909/233909126-48769505-adde-4982-beaf-2fe1635970f4.png)


### MBD File
  - Look into the file
```CSS
▶ strings backup.mdb
```
![image](https://user-images.githubusercontent.com/83878909/233927444-536ae3fa-9377-4efd-b6ac-783b4b7df837.png)

  - Extract Information
```CSS
▶ mdb-tables backup.mdb | grep --color=auto user
```
![image](https://user-images.githubusercontent.com/83878909/233927978-8404a46f-e088-4f4c-8d8c-5e6638269cbc.png)
```CSS
▶ mdb-export backup.mdb auth_user
```
![image](https://user-images.githubusercontent.com/83878909/233928307-60dc1282-0923-472e-a148-cdb5bedba4ea.png)

### Extract ZIP File Contents
```CSS
▶ 7z x Access\ Control.zip -p access4u@security
```
![image](https://user-images.githubusercontent.com/83878909/233932586-4b1e138c-13d7-4197-81ac-46189c7cd293.png)

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

