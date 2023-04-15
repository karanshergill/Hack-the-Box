# Hack the Box - Sauna

Add to DNS
```CSS
10.10.10.175    egotistical-bank.local sauna sauna.egotistical-bank.local
```

## Nmap
### TCP All Ports

```CSS
▶ nmap -Pn -sS -p- 10.10.10.175 -T4 --min-rate 1000 -oN surface.nmap

Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-15 09:39 IST
Nmap scan report for 10.10.10.175
Host is up (0.18s latency).
Not shown: 65515 filtered tcp ports (no-response)
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
49667/tcp open  unknown
49673/tcp open  unknown
49674/tcp open  unknown
49675/tcp open  unknown
49695/tcp open  unknown
49720/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 124.54 seconds
```

### Open TCP Ports Service Version and Default Scripts
```CSS
▶ nmap -sC -sV -p 53,80,88,135,139,389,445,464,593,636,3268,3269,5985,9389,49667,49673,49674,49675,49695,49720 10.10.10.175 -oN deep.nmap

Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-15 09:26 IST
Nmap scan report for 10.10.10.175
Host is up (0.18s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Egotistical Bank :: Home
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-04-15 10:56:16Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: EGOTISTICAL-BANK.LOCAL0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: EGOTISTICAL-BANK.LOCAL0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         Microsoft Windows RPC
49675/tcp open  msrpc         Microsoft Windows RPC
49695/tcp open  msrpc         Microsoft Windows RPC
49720/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: SAUNA; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 6h59m41s
| smb2-time: 
|   date: 2023-04-15T10:57:10
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 132.84 seconds
```

![image](https://user-images.githubusercontent.com/83878909/232182021-fe6ce919-1d8e-4fad-acdb-1925137c81bd.png)

---

## HTTP
### Home
![image](https://user-images.githubusercontent.com/83878909/232183100-b0ba710b-a0d0-456f-8428-866108bab641.png)

### Users
![image](https://user-images.githubusercontent.com/83878909/232183269-6ce5ead2-098a-42c1-a77b-99e9b68cce63.png)

```CSS
Fergus Smith
Shuan Coins
Sophie Driver
Bowie Taylor
Hugo Bear
Steven Kerb
```

---

## LDAPSearch
### Base DN (Distinguished Name)
```CSS
▶ ldapsearch -H ldap://10.10.10.175 -x -s base namingcontexts
```
![image](https://user-images.githubusercontent.com/83878909/232185487-95840fae-d92d-4a03-9795-cbddc1511dba.png)

### Subtree Attributes
```CSS
▶ ldapsearch -H ldap://10.10.10.175 -b 'DC=EGOTISTICAL-BANK,DC=LOCAL' -s sub
```
![image](https://user-images.githubusercontent.com/83878909/232194332-9d8dc461-a687-4416-a6f6-94b4d5b523e9.png)

---

## Kerberos
### Kerberos Authentication Attack
  - Identify valid users.
  - Create a wordlist of potential usernames using the names found earlier.

## Validate Usernames
```CSS
▶ kerbrute userenum --dc 10.10.10.175 -d egotistical-bank.local users.txt
```
![image](https://user-images.githubusercontent.com/83878909/232199517-5274525c-d5f5-4925-b2c9-5fc31b23082f.png)
```CSS
administrator@egotistical-bank.local
fsmith@egotistical-bank.local
```
### AS-REP Roasting
  - Find users who have Kerberos preauthentication disabled and get their NTLM hash.
```CSS
▶ 
```
---


