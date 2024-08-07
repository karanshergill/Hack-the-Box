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
