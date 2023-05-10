# Hack the Box - Support

```CSS
Machine IP: 10.10.11.174 - Windows
Difficulty: Easy
Category: OSCP Preparation
Vulnerabilities:
  - 
```

## Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

### Port Scan (TCP)
```CSS
▶ nmap -Pn -sS -O -p- 10.10.11.174 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.11.174
Host is up (0.17s latency).
Not shown: 65516 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
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
49664/tcp open  unknown
49668/tcp open  unknown
49674/tcp open  unknown
49676/tcp open  unknown
49703/tcp open  unknown
57664/tcp open  unknown
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2016 (85%)
OS CPE: cpe:/o:microsoft:windows_server_2016
Aggressive OS guesses: Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 135.87 seconds
```

## Service and Version Detection
```CSS

▶ nmap -Pn -sC -sV -p 53,88,135,389,445,464,593,636,3268,3269,5985,9389,49664,49668,49674,49676,49703,57664 10.10.11.174 -oN services.nmap

Nmap scan report for 10.10.11.174
Host is up (0.18s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-05-10 03:53:40Z)
135/tcp   open  msrpc         Microsoft Windows RPC
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: support.htb0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: support.htb0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
49664/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc         Microsoft Windows RPC
49703/tcp open  msrpc         Microsoft Windows RPC
57664/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-05-10T03:54:32
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required
|_clock-skew: -25s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 102.53 seconds
```

----

## Port 445 (SMB)
  - SMB enumeration.
  - List shares.
  - Check for null uthentication.
  - Check for anonymous authentication.

### SMB Enumeration
```CSS
▶ crackmapexec smb 10.10.11.174
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/b468b3d1-cda4-4c90-95f7-9da2c975dc7b)
  - Domain Controller(DC): `support.htb` 

### List SMB Shares
```CSS
▶ crackmapexec smb 10.10.11.174 --shares
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c4bc2e24-d78e-46b8-890d-0f5ba2e1a1a9)
  - No results.

### SMB Null Authentication
```
▶ crackmapexec smb --shares 10.10.11.174 -u '' -p ''
```
  - No results.

### SMB Anonymous Authentication
```CSS
▶ crackmapexec smb -u 'anonymous' -p ''
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ad0378f1-2068-41f9-9425-fd9f8e43ee7f)
  - Authenticated.

### List SMB Shares
  - List SMB shares as an anonymous user.
```CSS
▶ crackmapexec smb 10.10.11.174 --shares -u 'anonymous' -p ''
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1ba2510f-bdfa-45e9-9867-0fdd34b07360)

#### List Contents
  - List contents of the shared directory `support-tools`
  - Download `UserInfo.exe.zip` as it is not a common file.
```CSS
▶ smbclient -N //10.10.11.174/support-tools
▶ smb: \> dir
▶ smb: \> get UserInfo.exe.zip
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ed628e06-7e8d-4082-834c-6c0fef76b46c)

#### List Zip Contents
```CSS
▶ unzip -l UserInfo.exe.zip
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2fd08177-b803-4cfe-8cd0-e82a0eb24902)

#### Unzip Archieve
```CSS
▶ mkdir userinfo
▶ unzip UserInfo.exe.zip -d userinfo
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1624d058-b88b-4417-b134-6c393792701e)
```CSS
▶ tree
▶ file UserInfo.exe
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9859ca19-6a6e-4e08-9fe6-29dbf28d5b68)

---

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/006a73ab-227d-457f-b769-5f6daf98e776)

