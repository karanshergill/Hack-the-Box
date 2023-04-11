# Hack the Box - Forest

```CSS
Machine IP: 10.10.10.161
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- -T4 --min-rate 1000 10.10.10.161 -oG nmap.surface

Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-29 15:08 IST
Nmap scan report for 10.10.10.161
Host is up (0.10s latency).
Not shown: 65512 closed tcp ports (reset)
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
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49671/tcp open  unknown
49676/tcp open  unknown
49677/tcp open  unknown
49684/tcp open  unknown
49706/tcp open  unknown
```

```CSS
▶ nmap -sC -sV -p 53,88,135,139,389,445,464,593,636,3268,3269,5985,9389 10.10.10.161 -oG nmap.deep

Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-29 16:45 IST
Nmap scan report for forest.htb (10.10.10.161)
Host is up (0.087s latency). 
PORT     STATE SERVICE      VERSION
53/tcp   open  domain       Simple DNS Plus
88/tcp   open  kerberos-sec Microsoft Windows Kerberos (server time: 2023-03-29 11:22:23Z)
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp  open  kpasswd5?                                                
593/tcp  open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped                                               
3268/tcp open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped                                               
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found                                                 
9389/tcp open  mc-nmf       .NET Message Framing
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:                                                    
| smb2-security-mode:                                                   
|   311:                                                                
|_    Message signing enabled and required                              
| smb-security-mode:                                                    
|   account_used: <blank>                                               
|   authentication_level: user                                          
|   challenge_response: supported                                       
|_  message_signing: required                                           
|_clock-skew: mean: 2h26m52s, deviation: 4h02m30s, median: 6m51s
| smb-os-discovery:                                                     
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST                                               
|   NetBIOS computer name: FOREST\x00                                   
|   Domain name: htb.local                                              
|   Forest name: htb.local                                              
|   FQDN: FOREST.htb.local                                              
|_  System time: 2023-03-29T04:22:29-07:00                              
| smb2-time:                                                            
|   date: 2023-03-29T11:22:32                                           
|_  start_date: 2023-03-29T09:42:02                                     

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.23 seconds                      
```

---

