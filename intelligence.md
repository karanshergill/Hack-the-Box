# Hack the Box - Intelligence

```CSS
Nachine IP: 10.10.10.248
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.248 -T4 --min-rate 1000 -oN nmap.surface

Nmap scan report for 10.10.10.248
Host is up (0.18s latency).
Not shown: 65516 filtered tcp ports (no-response)
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
49691/tcp open  unknown
49692/tcp open  unknown
49707/tcp open  unknown
49714/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 304.78 seconds
```

```CSS
▶ nmap -sC -sV -p 53,80,88,135,139,389,445,464,593,636,3268,3269,5985,9389,49667,49691,49692,49707,49714 10.10.10.248 -oN nmap.deep

Nmap scan report for 10.10.10.248                                                                                                                                           
Host is up (0.18s latency).                                                                                                                                                 
                                                                                                                                                                            
PORT      STATE SERVICE       VERSION                                                                                                                                       
53/tcp    open  domain        Simple DNS Plus                                                                                                                               
80/tcp    open  http          Microsoft IIS httpd 10.0                                                                                                                      
| http-methods:                                                                                                                                                             
|_  Potentially risky methods: TRACE                                                                                                                                        
|_http-server-header: Microsoft-IIS/10.0                                                                                                                                    
|_http-title: Intelligence                                                                                                                                                  
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-04-10 09:15:40Z)                                                                                
135/tcp   open  msrpc         Microsoft Windows RPC                                                                                                                         
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn                                                                                                                 
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)                                           
|_ssl-date: 2023-04-10T09:17:11+00:00; +6h59m58s from scanner time.                                                                                                         
| ssl-cert: Subject: commonName=dc.intelligence.htb                                                                                                                         
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.intelligence.htb                                                                         
| Not valid before: 2021-04-19T00:43:16                                                                                                                                     
|_Not valid after:  2022-04-19T00:43:16                                                                                                                                     
445/tcp   open  microsoft-ds?                                                                                                                                               
464/tcp   open  kpasswd5?                                                                                                                                                   
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0                                                                                                           
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)                                           
|_ssl-date: 2023-04-10T09:17:12+00:00; +6h59m58s from scanner time.
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2023-04-10T09:17:11+00:00; +6h59m58s from scanner time.
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2023-04-10T09:17:12+00:00; +6h59m58s from scanner time.
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49691/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49692/tcp open  msrpc         Microsoft Windows RPC
49707/tcp open  msrpc         Microsoft Windows RPC
49714/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2023-04-10T09:16:35
|_  start_date: N/A
|_clock-skew: mean: 6h59m57s, deviation: 0s, median: 6h59m57s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 100.93 seconds
```

