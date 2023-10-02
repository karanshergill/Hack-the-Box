# Hack the Box - Forge

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.111 -- -Pn
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
Open 10.10.11.111:22
Open 10.10.11.111:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.11.111
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 10:26 IST
Initiating Parallel DNS resolution of 1 host. at 10:26
Completed Parallel DNS resolution of 1 host. at 10:26, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:26
Scanning 10.10.11.111 [2 ports]
Discovered open port 22/tcp on 10.10.11.111
Discovered open port 80/tcp on 10.10.11.111
Completed Connect Scan at 10:26, 0.15s elapsed (2 total ports)
Nmap scan report for 10.10.11.111
Host is up, received user-set (0.15s latency).
Scanned at 2023-10-02 10:26:42 IST for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds
```

```shell
rustscan -u 5000 -p 22,80 -a 10.10.11.111 -- -Pn -sC -sV
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
Open 10.10.11.111:22
Open 10.10.11.111:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn -sC -sV" on ip 10.10.11.111
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 10:28 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 10:28
Completed Parallel DNS resolution of 1 host. at 10:28, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:28
Scanning 10.10.11.111 [2 ports]
Discovered open port 80/tcp on 10.10.11.111
Discovered open port 22/tcp on 10.10.11.111
Completed Connect Scan at 10:28, 0.15s elapsed (2 total ports)
Initiating Service scan at 10:28
Scanning 2 services on 10.10.11.111
Completed Service scan at 10:28, 6.30s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.11.111.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 4.33s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.60s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
Nmap scan report for 10.10.11.111
Host is up, received user-set (0.15s latency).
Scanned at 2023-10-02 10:28:27 IST for 11s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 4f:78:65:66:29:e4:87:6b:3c:cc:b4:3a:d2:57:20:ac (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC2sK9Bs3bKpmIER8QElFzWVwM0V/pval09g7BOCYMOZihHpPeE4S2aCt0oe9/KHyALDgtRb3++WLuaI6tdYA1k4bhZU/0bPENKBp6ykWUsWieSSarmd0sfekrbcqob69pUJSxIVzLrzXbg4CWnnLh/UMLc3emGkXxjLOkR1APIZff3lXIDr8j2U3vDAwgbQINDinJaFTjDcXkOY57u4s2Si4XjJZnQVXuf8jGZxyyMKY/L/RYxRiZVhDGzEzEBxyLTgr5rHi3RF+mOtzn3s5oJvVSIZlh15h2qoJX1v7N/N5/7L1RR9rV3HZzDT+reKtdgUHEAKXRdfrff04hXy6aepQm+kb4zOJRiuzZSw6ml/N0ITJy/L6a88PJflpctPU4XKmVX5KxMasRKlRM4AMfzrcJaLgYYo1bVC9Ik+cCt7UjtvIwNZUcNMzFhxWFYFPhGVJ4HC0Cs2AuUC8T0LisZfysm61pLRUGP7ScPo5IJhwlMxncYgFzDrFRig3DlFQ0=
|   256 79:df:3a:f1:fe:87:4a:57:b0:fd:4e:d0:54:c6:28:d9 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBH67/BaxpvT3XsefC62xfP5fvtcKxG2J2di6u8wupaiDIPxABb5/S1qecyoQJYGGJJOHyKlVdqgF1Odf2hAA69Y=
|   256 b0:58:11:40:6d:8c:bd:c5:72:aa:83:08:c5:51:fb:33 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILcTSbyCdqkw29aShdKmVhnudyA2B6g6ULjspAQpHLIC
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Did not follow redirect to http://forge.htb
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:28
Completed NSE at 10:28, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.74 seconds
```

TCP 80: HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9298fe1e-5e8a-42e7-a84f-b18c14604d07)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/285334ee-5f76-4ba2-a309-b1b300de5689)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/53e4d0eb-d059-41c5-8440-26b9758308c1)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7812a2c1-cef1-4903-9315-15016492ebe2)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e660be1e-be06-4fb4-8507-64aa67e4c5e1)

```shell
feroxbuster -u http://forge.htb -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-small-words.txt -s 200 -n
```
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://forge.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/seclists/Discovery/Web-Content/raft-small-words.txt
 👌  Status Codes          │ [200]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.10.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🚫  Do Not Recurse        │ true
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
200      GET       56l      102w      874c http://forge.htb/static/css/main.css
200      GET       33l       58w      929c http://forge.htb/upload
200      GET       26l       64w      963c http://forge.htb/static/js/main.js
200      GET       39l       66w      553c http://forge.htb/static/css/upload.css
200      GET      737l     3629w   289124c http://forge.htb/static/images/image9.jpg
200      GET      583l     3316w   262102c http://forge.htb/static/images/image5.jpg
200      GET      467l     2872w   259443c http://forge.htb/static/images/image3.jpg
200      GET     1050l     6302w   461659c http://forge.htb/static/images/image2.jpg
200      GET     1068l     5977w   438325c http://forge.htb/static/images/image4.jpg
200      GET     1570l     8945w   698879c http://forge.htb/static/images/image8.jpg
200      GET     2355l    12931w  1041359c http://forge.htb/static/images/image1.jpg
200      GET       72l       92w     2050c http://forge.htb/
[####################] - 2m     43030/43030   0s      found:12      errors:18     
[####################] - 2m     43008/43008   322/s   http://forge.htb/  
```

Virtual Host Bure-force
```shell
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.forge.htb" -u http://forge.htb -mc 200
```
```shell
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://forge.htb
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Header           : Host: FUZZ.forge.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200
________________________________________________

[Status: 200, Size: 27, Words: 4, Lines: 2, Duration: 683ms]
    * FUZZ: admin

:: Progress: [4990/4990] :: Job [1/1] :: 269 req/sec :: Duration: [0:00:19] :: Errors: 0 ::
```
