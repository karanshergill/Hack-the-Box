# Hack the Box - Cascade

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.182 -- -Pn
```

```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.                                                                                                                    
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |                                                                                                                    
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |                                                                                                                    
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'                                                                                                                    
The Modern Day Port Scanner.                                                                                                                                                
________________________________________                                                                                                                                    
: http://discord.skerritt.blog           :                                                                                                                                  
: https://github.com/RustScan/RustScan :                                                                                                                                    
 --------------------------------------                                                                                                                                     
🌍HACK THE PLANET🌍                                                                                                                                                         
                                                                                                                                                                            
[~] The config file is expected to be at "/home/superuser/.rustscan.toml"                                                                                                   
[~] Automatically increasing ulimit value to 5000.                                                                                                                          
Open 10.10.10.182:53                                                                                                                                                        
Open 10.10.10.182:88                                                                                                                                                        
Open 10.10.10.182:135                                                                                                                                                       
Open 10.10.10.182:139                                                                                                                                                       
Open 10.10.10.182:389                                                                                                                                                       
Open 10.10.10.182:445                                                                                                                                                       
Open 10.10.10.182:636                                                                                                                                                       
Open 10.10.10.182:3268                                                                                                                                                      
Open 10.10.10.182:3269                                                                                                                                                      
Open 10.10.10.182:5985                                                                                                                                                      
Open 10.10.10.182:49154                                                                                                                                                     
Open 10.10.10.182:49155                                                                                                                                                     
Open 10.10.10.182:49157                                                                                                                                                     
Open 10.10.10.182:49158                                                                                                                                                     
Open 10.10.10.182:49170                                                                                                                                                     
[~] Starting Script(s)                                                                                                                                                      
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.10.182                                                                                                    
Depending on the complexity of the script, results may take some time to appear.                                                                                            
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.                                                                              
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-28 13:05 IST                                                                                                         
Initiating Parallel DNS resolution of 1 host. at 13:05                                                                                                                      
Completed Parallel DNS resolution of 1 host. at 13:05, 0.00s elapsed                                                                                                        
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]                                                                            
Initiating Connect Scan at 13:05                                                                                                                                            
Scanning 10.10.10.182 [15 ports]
Discovered open port 135/tcp on 10.10.10.182                                                                                                                                
Discovered open port 53/tcp on 10.10.10.182                                                                                                                                 
Discovered open port 445/tcp on 10.10.10.182
Discovered open port 139/tcp on 10.10.10.182
Discovered open port 49157/tcp on 10.10.10.182
Discovered open port 636/tcp on 10.10.10.182
Discovered open port 3268/tcp on 10.10.10.182
Discovered open port 3269/tcp on 10.10.10.182
Discovered open port 49154/tcp on 10.10.10.182
Discovered open port 5985/tcp on 10.10.10.182
Discovered open port 88/tcp on 10.10.10.182 
Discovered open port 49155/tcp on 10.10.10.182
Discovered open port 49158/tcp on 10.10.10.182
Discovered open port 389/tcp on 10.10.10.182
Discovered open port 49170/tcp on 10.10.10.182
Completed Connect Scan at 13:05, 0.31s elapsed (15 total ports)
Nmap scan report for 10.10.10.182
Host is up, received user-set (0.15s latency).
Scanned at 2023-09-28 13:05:56 IST for 1s

PORT      STATE SERVICE          REASON
53/tcp    open  domain           syn-ack
88/tcp    open  kerberos-sec     syn-ack
135/tcp   open  msrpc            syn-ack
139/tcp   open  netbios-ssn      syn-ack
389/tcp   open  ldap             syn-ack
445/tcp   open  microsoft-ds     syn-ack
636/tcp   open  ldapssl          syn-ack
3268/tcp  open  globalcatLDAP    syn-ack
3269/tcp  open  globalcatLDAPssl syn-ack
5985/tcp  open  wsman            syn-ack
49154/tcp open  unknown          syn-ack
49155/tcp open  unknown          syn-ack
49157/tcp open  unknown          syn-ack
49158/tcp open  unknown          syn-ack
49170/tcp open  unknown          syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.36 seconds
```

Open Ports: 53,88,135,139,389,445,636,3269,3268,5985,49154,49157,49155,49158,49170

```shell
rustscan -u 5000 -a 10.10.10.182 -p 53,88,135,139,389,445,636,3269,3268,5985,49154,49157,49155,49158,49170 -- -Pn -sC -sV
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
0day was here ♥

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.182:53
Open 10.10.10.182:445
Open 10.10.10.182:135
Open 10.10.10.182:389
Open 10.10.10.182:88
Open 10.10.10.182:139
Open 10.10.10.182:5985
Open 10.10.10.182:3269
Open 10.10.10.182:3268
Open 10.10.10.182:636
Open 10.10.10.182:49154
Open 10.10.10.182:49157
Open 10.10.10.182:49155
Open 10.10.10.182:49158
Open 10.10.10.182:49170
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn -sC -sV" on ip 10.10.10.182
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-28 13:11 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 13:11
Completed NSE at 13:11, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 13:11
Completed NSE at 13:11, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 13:11
Completed NSE at 13:11, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 13:11
Completed Parallel DNS resolution of 1 host. at 13:11, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 13:11
Scanning 10.10.10.182 [15 ports]
Discovered open port 135/tcp on 10.10.10.182
Discovered open port 139/tcp on 10.10.10.182
Discovered open port 53/tcp on 10.10.10.182
Discovered open port 445/tcp on 10.10.10.182
Discovered open port 5985/tcp on 10.10.10.182
Discovered open port 49154/tcp on 10.10.10.182
Discovered open port 49170/tcp on 10.10.10.182
Discovered open port 49155/tcp on 10.10.10.182
Discovered open port 636/tcp on 10.10.10.182
Discovered open port 389/tcp on 10.10.10.182
Discovered open port 3268/tcp on 10.10.10.182
Discovered open port 3269/tcp on 10.10.10.182
Discovered open port 88/tcp on 10.10.10.182
Discovered open port 49158/tcp on 10.10.10.182
Discovered open port 49157/tcp on 10.10.10.182
Completed Connect Scan at 13:11, 0.31s elapsed (15 total ports)
Initiating Service scan at 13:11
Scanning 15 services on 10.10.10.182
Completed Service scan at 13:12, 56.15s elapsed (15 services on 1 host)
NSE: Script scanning 10.10.10.182.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 13:12
NSE Timing: About 99.95% done; ETC: 13:12 (0:00:00 remaining)
Completed NSE at 13:12, 40.11s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 13:12
Completed NSE at 13:12, 4.32s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 13:12
Completed NSE at 13:12, 0.00s elapsed
Nmap scan report for 10.10.10.182
Host is up, received user-set (0.15s latency).
Scanned at 2023-09-28 13:11:18 IST for 101s

PORT      STATE SERVICE       REASON  VERSION
53/tcp    open  domain        syn-ack Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
| dns-nsid: 
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15D39)
88/tcp    open  kerberos-sec  syn-ack Microsoft Windows Kerberos (server time: 2023-09-28 07:41:25Z)
135/tcp   open  msrpc         syn-ack Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: cascade.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack
636/tcp   open  tcpwrapped    syn-ack
3268/tcp  open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: cascade.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack
5985/tcp  open  http          syn-ack Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49154/tcp open  msrpc         syn-ack Microsoft Windows RPC
49155/tcp open  msrpc         syn-ack Microsoft Windows RPC
49157/tcp open  ncacn_http    syn-ack Microsoft Windows RPC over HTTP 1.0
49158/tcp open  msrpc         syn-ack Microsoft Windows RPC
49170/tcp open  msrpc         syn-ack Microsoft Windows RPC
Service Info: Host: CASC-DC1; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-09-28T07:42:16
|_  start_date: 2023-09-28T07:29:55
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled and required
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 51409/tcp): CLEAN (Timeout)
|   Check 2 (port 61421/tcp): CLEAN (Timeout)
|   Check 3 (port 10882/udp): CLEAN (Timeout)
|   Check 4 (port 25286/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: 0s

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 13:12
Completed NSE at 13:12, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 13:12
Completed NSE at 13:12, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 13:12
Completed NSE at 13:12, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 101.11 seconds
```

### SMB
```shell
root@kali# smbclient -N -L //10.10.10.182
```
```shell
Anonymous login successful

        Sharename       Type      Comment
        ---------       ----      -------
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.10.10.182 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

```
