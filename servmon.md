```CSS
rustscan -a 10.10.10.184 -r 0-65535 --ulimit 5000
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
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.184:22
Open 10.10.10.184:21
Open 10.10.10.184:80
Open 10.10.10.184:135
Open 10.10.10.184:139
Open 10.10.10.184:445
Open 10.10.10.184:6699
Open 10.10.10.184:8443
Open 10.10.10.184:49670
Open 10.10.10.184:49669
Open 10.10.10.184:49668
Open 10.10.10.184:49667
Open 10.10.10.184:49665
Open 10.10.10.184:49664
Open 10.10.10.184:49666
[~] Starting Script(s)
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-19 10:26 IST
Initiating Ping Scan at 10:26
Scanning 10.10.10.184 [2 ports]
Completed Ping Scan at 10:26, 0.15s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:26
Completed Parallel DNS resolution of 1 host. at 10:26, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:26
Scanning 10.10.10.184 [15 ports]
Discovered open port 445/tcp on 10.10.10.184
Discovered open port 22/tcp on 10.10.10.184
Discovered open port 80/tcp on 10.10.10.184
Discovered open port 139/tcp on 10.10.10.184
Discovered open port 21/tcp on 10.10.10.184
Discovered open port 135/tcp on 10.10.10.184
Discovered open port 49664/tcp on 10.10.10.184
Discovered open port 6699/tcp on 10.10.10.184
Discovered open port 49669/tcp on 10.10.10.184
Discovered open port 49668/tcp on 10.10.10.184
Discovered open port 49666/tcp on 10.10.10.184
Discovered open port 49670/tcp on 10.10.10.184
Discovered open port 49665/tcp on 10.10.10.184
Discovered open port 49667/tcp on 10.10.10.184
Discovered open port 8443/tcp on 10.10.10.184
Completed Connect Scan at 10:26, 0.31s elapsed (15 total ports)
Nmap scan report for 10.10.10.184
Host is up, received syn-ack (0.15s latency).
Scanned at 2023-09-19 10:26:35 IST for 0s

PORT      STATE SERVICE      REASON
21/tcp    open  ftp          syn-ack
22/tcp    open  ssh          syn-ack
80/tcp    open  http         syn-ack
135/tcp   open  msrpc        syn-ack
139/tcp   open  netbios-ssn  syn-ack
445/tcp   open  microsoft-ds syn-ack
6699/tcp  open  napster      syn-ack
8443/tcp  open  https-alt    syn-ack
49664/tcp open  unknown      syn-ack
49665/tcp open  unknown      syn-ack
49666/tcp open  unknown      syn-ack
49667/tcp open  unknown      syn-ack
49668/tcp open  unknown      syn-ack
49669/tcp open  unknown      syn-ack
49670/tcp open  unknown      syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.49 seconds
```

```CSS
nmap -sC -sV 10.10.10.184 -p 21,22,80,135,445,6699,8443,49664-49670
```
```CSS

```
FTP:21
Anonymous Authentication
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2f035b58-c3a9-4916-a41a-a6b8b6ac56f1)

File `User\Nadine\Confidential.txt`
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3e72ed0e-42bf-459f-b5df-b04d0eff3acb)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/804dd021-5bd9-4367-8eb3-c87c39c152d4)

File `User\Nathan\Notes to do.txt`
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cd8f8766-ee47-489a-84b7-28be57b8a207)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5d24a73c-3278-4454-bbfe-4ce87a4ffe86)

HTTP:80
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9e16766d-8877-4ae0-8d00-330fae6cf5fb)
