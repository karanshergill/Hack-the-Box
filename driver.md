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

Firmware Update
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/29efdec0-7744-4955-a5ea-1e2cdedc0d10)
