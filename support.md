# Hack the Box - Support

## Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.174 -- -Pn
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Please contribute more quotes to our GitHub https://github.com/rustscan/rustscan

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.174:53
Open 10.10.11.174:88
Open 10.10.11.174:135
Open 10.10.11.174:139
Open 10.10.11.174:389
Open 10.10.11.174:445
Open 10.10.11.174:464
Open 10.10.11.174:593
Open 10.10.11.174:636
Open 10.10.11.174:3269
Open 10.10.11.174:3268
Open 10.10.11.174:5985
Open 10.10.11.174:9389
Open 10.10.11.174:49664
Open 10.10.11.174:49667
Open 10.10.11.174:49674
Open 10.10.11.174:49686
Open 10.10.11.174:49700
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-06 16:47 IST
Initiating Parallel DNS resolution of 1 host. at 16:47
Completed Parallel DNS resolution of 1 host. at 16:47, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 16:47
Scanning 10.10.11.174 [18 ports]
Discovered open port 445/tcp on 10.10.11.174
Discovered open port 53/tcp on 10.10.11.174
Discovered open port 139/tcp on 10.10.11.174
Discovered open port 3269/tcp on 10.10.11.174
Discovered open port 135/tcp on 10.10.11.174
Discovered open port 3268/tcp on 10.10.11.174
Discovered open port 593/tcp on 10.10.11.174
Discovered open port 5985/tcp on 10.10.11.174
Discovered open port 464/tcp on 10.10.11.174
Discovered open port 9389/tcp on 10.10.11.174
Discovered open port 49686/tcp on 10.10.11.174
Discovered open port 49664/tcp on 10.10.11.174
Discovered open port 389/tcp on 10.10.11.174
Discovered open port 88/tcp on 10.10.11.174
Discovered open port 49700/tcp on 10.10.11.174
Discovered open port 49667/tcp on 10.10.11.174
Discovered open port 49674/tcp on 10.10.11.174
Discovered open port 636/tcp on 10.10.11.174
Completed Connect Scan at 16:47, 0.33s elapsed (18 total ports)
Nmap scan report for 10.10.11.174
Host is up, received user-set (0.16s latency).
Scanned at 2023-10-06 16:47:45 IST for 0s

PORT      STATE SERVICE          REASON
53/tcp    open  domain           syn-ack
88/tcp    open  kerberos-sec     syn-ack
135/tcp   open  msrpc            syn-ack
139/tcp   open  netbios-ssn      syn-ack
389/tcp   open  ldap             syn-ack
445/tcp   open  microsoft-ds     syn-ack
464/tcp   open  kpasswd5         syn-ack
593/tcp   open  http-rpc-epmap   syn-ack
636/tcp   open  ldapssl          syn-ack
3268/tcp  open  globalcatLDAP    syn-ack
3269/tcp  open  globalcatLDAPssl syn-ack
5985/tcp  open  wsman            syn-ack
9389/tcp  open  adws             syn-ack
49664/tcp open  unknown          syn-ack
49667/tcp open  unknown          syn-ack
49674/tcp open  unknown          syn-ack
49686/tcp open  unknown          syn-ack
49700/tcp open  unknown          syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.37 seconds
```

```shell
rustscan -u 5000 -p 53,88,135,139,389,445,464,593,636,3269,3268,5985,9389 -a 10.10.11.174 -- -Pn -sC -sV
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.174:53
Open 10.10.11.174:88
Open 10.10.11.174:389
Open 10.10.11.174:139
Open 10.10.11.174:135
Open 10.10.11.174:445
Open 10.10.11.174:593
Open 10.10.11.174:636
Open 10.10.11.174:3269
Open 10.10.11.174:464
Open 10.10.11.174:3268
Open 10.10.11.174:5985
Open 10.10.11.174:9389
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-06 16:53 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:53
Completed NSE at 16:53, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:53
Completed NSE at 16:53, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:53
Completed NSE at 16:53, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 16:53
Completed Parallel DNS resolution of 1 host. at 16:53, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 16:53
Scanning 10.10.11.174 [13 ports]
Discovered open port 139/tcp on 10.10.11.174
Discovered open port 53/tcp on 10.10.11.174
Discovered open port 135/tcp on 10.10.11.174
Discovered open port 445/tcp on 10.10.11.174
Discovered open port 5985/tcp on 10.10.11.174
Discovered open port 88/tcp on 10.10.11.174
Discovered open port 389/tcp on 10.10.11.174
Discovered open port 3268/tcp on 10.10.11.174
Discovered open port 593/tcp on 10.10.11.174
Discovered open port 9389/tcp on 10.10.11.174
Discovered open port 636/tcp on 10.10.11.174
Discovered open port 464/tcp on 10.10.11.174
Discovered open port 3269/tcp on 10.10.11.174
Completed Connect Scan at 16:53, 0.34s elapsed (13 total ports)
Initiating Service scan at 16:53
Scanning 13 services on 10.10.11.174
Completed Service scan at 16:54, 15.27s elapsed (13 services on 1 host)
NSE: Script scanning 10.10.11.174.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:54
NSE Timing: About 99.94% done; ETC: 16:54 (0:00:00 remaining)
Completed NSE at 16:54, 40.09s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:54
Completed NSE at 16:54, 4.91s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:54
Completed NSE at 16:54, 0.00s elapsed
Nmap scan report for 10.10.11.174
Host is up, received user-set (0.17s latency).
Scanned at 2023-10-06 16:53:53 IST for 61s

PORT     STATE SERVICE       REASON  VERSION
53/tcp   open  domain        syn-ack Simple DNS Plus
88/tcp   open  kerberos-sec  syn-ack Microsoft Windows Kerberos (server time: 2023-10-06 11:24:01Z)
135/tcp  open  msrpc         syn-ack Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: support.htb0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds? syn-ack
464/tcp  open  kpasswd5?     syn-ack
593/tcp  open  ncacn_http    syn-ack Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack
3268/tcp open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: support.htb0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack
5985/tcp open  http          syn-ack Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp open  mc-nmf        syn-ack .NET Message Framing
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 19493/tcp): CLEAN (Timeout)
|   Check 2 (port 14647/tcp): CLEAN (Timeout)
|   Check 3 (port 45724/udp): CLEAN (Timeout)
|   Check 4 (port 20897/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2023-10-06T11:24:13
|_  start_date: N/A
|_clock-skew: 0s

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:54
Completed NSE at 16:54, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:54
Completed NSE at 16:54, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:54
Completed NSE at 16:54, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 60.95 seconds
```

```shell
echo "10.10.11.174    dc.dupport.htb support.htb" | sudo tee -a /etc/hosts
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

#### Unzip Archive
```CSS
▶ mkdir userinfo
▶ unzip UserInfo.exe.zip -d userinfo
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1624d058-b88b-4417-b134-6c393792701e)

```CSS
▶ tree
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9859ca19-6a6e-4e08-9fe6-29dbf28d5b68)

```CSS
▶ file UserInfo.exe
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a4ed6261-20bd-46ee-b5a0-5c04b62e8691)

---

### Decompile EXE File
  - Decompile `UserInfo.exe` using `ILSpy` to read the source code.
  - Open the file `UserInfo.exe` in `ILSpy`. 
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/006a73ab-227d-457f-b769-5f6daf98e776)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2443765c-1eec-4efb-9285-66d32009753e)

  - LDAP Credentials:  
