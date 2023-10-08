# Hack the Box - Holiday

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.25 -- -Pn
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
Open 10.10.10.25:22
Open 10.10.10.25:8000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-08 12:45 EDT
Initiating Parallel DNS resolution of 1 host. at 12:45
Completed Parallel DNS resolution of 1 host. at 12:45, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:45
Scanning 10.10.10.25 [2 ports]
Discovered open port 8000/tcp on 10.10.10.25
Discovered open port 22/tcp on 10.10.10.25
Completed Connect Scan at 12:45, 0.14s elapsed (2 total ports)
Nmap scan report for 10.10.10.25
Host is up, received user-set (0.14s latency).
Scanned at 2023-10-08 12:45:50 EDT for 0s

PORT     STATE SERVICE  REASON
22/tcp   open  ssh      syn-ack
8000/tcp open  http-alt syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.21 seconds
```

```shell
rustscan -u 5000 -p 22,8000 -a 10.10.10.25 -- -Pn -sCV
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
Open 10.10.10.25:22
Open 10.10.10.25:8000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-08 16:08 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 16:08
Completed Parallel DNS resolution of 1 host. at 16:08, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 16:08
Scanning 10.10.10.25 [2 ports]
Discovered open port 22/tcp on 10.10.10.25
Discovered open port 8000/tcp on 10.10.10.25
Completed Connect Scan at 16:08, 0.14s elapsed (2 total ports)
Initiating Service scan at 16:08
Scanning 2 services on 10.10.10.25
Completed Service scan at 16:08, 11.47s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.10.25.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 4.29s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.58s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
Nmap scan report for 10.10.10.25
Host is up, received user-set (0.14s latency).
Scanned at 2023-10-08 16:08:35 EDT for 17s

PORT     STATE SERVICE REASON  VERSION
22/tcp   open  ssh     syn-ack OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c3:aa:3d:bd:0e:01:46:c9:6b:46:73:f3:d1:ba:ce:f2 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCxRUV+xkboQ0we+UPL74vCCLSGysv5NntdVnMMzyEDtUPe09iiknmsFAb8uEnpF+u1T5im1uFxhKnusM+Zhi8l8OiBsjojUWew2zAy4wC0p8qpplh3D1Viex8ybvcQZlwweLbwV8zHoTOV06JAQLR4y/0zAnD5By0EcxdUXzZQJox1NFQ6FaU/5qHE8WjnA34uMyl9rt0y1DEVUh7w3nwR2FqjBoh1i+/8VDHcvoQDmY2kh/XSxruJzswUxvk24cTFAWt2Y+BZbzOhsGF3KLq71nAKYrRiD9uja0j0l9SVX5XWHQ33mSjv52WrFca3s1MSAJzK+Ql5ZVxBVJEJlNvN
|   256 b5:67:f5:eb:8d:11:e9:0f:dd:f4:52:25:9f:b1:2f:23 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOi8Okv0YxMiWPRJHRhhR8V5e82TnWrFEoOLmlZiwVY98GnudcVs3BRnbV7b7tnfxRdeafS4yPuVtYSYpRpE9U8=
|   256 79:e9:78:96:c5:a8:f4:02:83:90:58:3f:e5:8d:fa:98 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKrKLpZ3M2QSMqW28gvO6iH3imEsWNaEkeM2d6MtVThp
8000/tcp open  http    syn-ack Node.js Express framework
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Error
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:08
Completed NSE at 16:08, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.82 seconds
```

```shell
feroxbuster -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt --no-recursion --dont-extract-links -u http://10.10.10.25:8000 --random-agent```
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.10.25:8000
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ Random
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🏁  HTTP methods          │ [GET]
 🚫  Do Not Recurse        │ true
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET       10l       15w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET       18l       38w      621c http://10.10.10.25:8000/
301      GET        9l       15w      165c http://10.10.10.25:8000/css => http://10.10.10.25:8000/css/
302      GET        1l        4w       28c http://10.10.10.25:8000/admin => http://10.10.10.25:8000/login
302      GET        1l        4w       28c http://10.10.10.25:8000/logout => http://10.10.10.25:8000/login
200      GET       30l       78w     1171c http://10.10.10.25:8000/login
302      GET        1l        4w       28c http://10.10.10.25:8000/agent => http://10.10.10.25:8000/login
[####################] - 79s    26584/26584   0s      found:6       errors:0      
[####################] - 78s    26584/26584   340/s   http://10.10.10.25:8000/     
```

TCP 8000
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2d7b8665-72f3-4208-b93d-2052e429b879)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/249197b9-330a-4c99-87b8-d3cac61b9ce4)

