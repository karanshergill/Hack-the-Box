# Hack the Box - Help

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.121 -- -Pn
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
Open 10.10.10.121:22
Open 10.10.10.121:80
Open 10.10.10.121:3000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-09 02:44 EDT
Initiating Parallel DNS resolution of 1 host. at 02:44
Completed Parallel DNS resolution of 1 host. at 02:44, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 02:44
Scanning 10.10.10.121 [3 ports]
Discovered open port 80/tcp on 10.10.10.121
Discovered open port 22/tcp on 10.10.10.121
Discovered open port 3000/tcp on 10.10.10.121
Completed Connect Scan at 02:44, 0.15s elapsed (3 total ports)
Nmap scan report for 10.10.10.121
Host is up, received user-set (0.15s latency).
Scanned at 2023-10-09 02:44:36 EDT for 0s

PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack
80/tcp   open  http    syn-ack
3000/tcp open  ppp     syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.23 seconds
```
```shell
rustscan -u 5000 -p 22,80,3000 -a 10.10.10.121 -- -Pn -sCV
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
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.121:22
Open 10.10.10.121:80
Open 10.10.10.121:3000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-09 02:48 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 02:48
Completed Parallel DNS resolution of 1 host. at 02:48, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 02:48
Scanning 10.10.10.121 [3 ports]
Discovered open port 80/tcp on 10.10.10.121
Discovered open port 3000/tcp on 10.10.10.121
Discovered open port 22/tcp on 10.10.10.121
Completed Connect Scan at 02:48, 0.14s elapsed (3 total ports)
Initiating Service scan at 02:48
Scanning 3 services on 10.10.10.121
Completed Service scan at 02:48, 11.57s elapsed (3 services on 1 host)
NSE: Script scanning 10.10.10.121.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 4.76s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.59s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
Nmap scan report for 10.10.10.121
Host is up, received user-set (0.14s latency).
Scanned at 2023-10-09 02:48:28 EDT for 17s

PORT     STATE SERVICE REASON  VERSION
22/tcp   open  ssh     syn-ack OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e5:bb:4d:9c:de:af:6b:bf:ba:8c:22:7a:d8:d7:43:28 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCZY4jlvWqpdi8bJPUnSkjWmz92KRwr2G6xCttorHM8Rq2eCEAe1ALqpgU44L3potYUZvaJuEIsBVUSPlsKv+ds8nS7Mva9e9ztlad/fzBlyBpkiYxty+peoIzn4lUNSadPLtYH6khzN2PwEJYtM/b6BLlAAY5mDsSF0Cz3wsPbnu87fNdd7WO0PKsqRtHpokjkJ22uYJoDSAM06D7uBuegMK/sWTVtrsDakb1Tb6H8+D0y6ZQoE7XyHSqD0OABV3ON39GzLBOnob4Gq8aegKBMa3hT/Xx9Iac6t5neiIABnG4UP03gm207oGIFHvlElGUR809Q9qCJ0nZsup4bNqa/
|   256 d5:b0:10:50:74:86:a3:9f:c5:53:6f:3b:4a:24:61:19 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBHINVMyTivG0LmhaVZxiIESQuWxvN2jt87kYiuPY2jyaPBD4DEt8e/1kN/4GMWj1b3FE7e8nxCL4PF/lR9XjEis=
|   256 e2:1b:88:d3:76:21:d4:1e:38:15:4a:81:11:b7:99:07 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHxDPln3rCQj04xFAKyecXJaANrW3MBZJmbhtL4SuDYX
80/tcp   open  http    syn-ack Apache httpd 2.4.18
|_http-title: Did not follow redirect to http://help.htb/
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
3000/tcp open  http    syn-ack Node.js Express framework
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Site doesn't have a title (application/json; charset=utf-8).
Service Info: Host: 127.0.1.1; OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 02:48
Completed NSE at 02:48, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.36 seconds
```

TCP 80 - HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a98828d4-4165-4b0e-98d2-2076cc3fed22)

```shell
feroxbuster -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt --no-recursion --dont-extract-links -u http://help.htb/support --random-agent
```
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://help.htb/support
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
403      GET       11l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
404      GET        9l       32w        -c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
301      GET        9l       28w      313c http://help.htb/support/images => http://help.htb/support/images/
301      GET        9l       28w      306c http://help.htb/support => http://help.htb/support/
301      GET        9l       28w      309c http://help.htb/support/js => http://help.htb/support/js/
301      GET        9l       28w      315c http://help.htb/support/includes => http://help.htb/support/includes/
301      GET        9l       28w      314c http://help.htb/support/uploads => http://help.htb/support/uploads/
301      GET        9l       28w      310c http://help.htb/support/css => http://help.htb/support/css/
301      GET        9l       28w      312c http://help.htb/support/views => http://help.htb/support/views/
301      GET        9l       28w      318c http://help.htb/support/controllers => http://help.htb/support/controllers/
404      GET        9l       33w      292c http://help.htb/support/reports%20list
404      GET        9l       33w      294c http://help.htb/support/external%20files
404      GET        9l       33w      293c http://help.htb/support/style%20library
404      GET        9l       33w      290c http://help.htb/support/modern%20mom
404      GET        9l       34w      295c http://help.htb/support/neuf%20giga%20photo
404      GET        9l       33w      294c http://help.htb/support/web%20references
404      GET        9l       33w      290c http://help.htb/support/my%20project
404      GET        9l       33w      290c http://help.htb/support/contact%20us
404      GET        9l       33w      291c http://help.htb/support/donate%20cash
404      GET        9l       33w      289c http://help.htb/support/home%20page
404      GET        9l       33w      294c http://help.htb/support/press%20releases
404      GET        9l       33w      294c http://help.htb/support/privacy%20policy
404      GET        9l       33w      294c http://help.htb/support/planned%20giving
404      GET        9l       33w      288c http://help.htb/support/site%20map
404      GET        9l       33w      288c http://help.htb/support/about%20us
404      GET        9l       33w      292c http://help.htb/support/bequest%20gift
404      GET        9l       33w      289c http://help.htb/support/gift%20form
404      GET        9l       34w      296c http://help.htb/support/life%20income%20gift
404      GET        9l       33w      290c http://help.htb/support/new%20folder
404      GET        9l       33w      291c http://help.htb/support/site%20assets
404      GET        9l       34w      291c http://help.htb/support/what%20is%20new
[####################] - 87s    26584/26584   0s      found:29      errors:0      
[####################] - 86s    26584/26584   307/s   http://help.htb/support/    
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b2fe2ec8-f2bb-4e2c-92b6-af15b77ea7ac)

Exploits
```shell
searchsploit helpdeskz
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/38476700-c1d5-402e-b5e2-01fa9ca93c82)

