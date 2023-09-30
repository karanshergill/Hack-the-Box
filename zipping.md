# HAck the Box - Zipping

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.229 -- -Pn
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
Open 10.10.11.229:22
Open 10.10.11.229:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.11.229
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-30 09:22 IST
Initiating Parallel DNS resolution of 1 host. at 09:22
Completed Parallel DNS resolution of 1 host. at 09:22, 0.00s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 09:22
Scanning 10.10.11.229 [2 ports]
Discovered open port 80/tcp on 10.10.11.229
Discovered open port 22/tcp on 10.10.11.229
Completed Connect Scan at 09:22, 0.14s elapsed (2 total ports)
Nmap scan report for 10.10.11.229
Host is up, received user-set (0.14s latency).
Scanned at 2023-09-30 09:22:16 IST for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.19 seconds
```

```shell
rustscan -u 5000 -a 10.10.11.229 -p 22,80 -- -Pn -sC -sV
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
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.229:22
Open 10.10.11.229:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn -sC -sV" on ip 10.10.11.229
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-30 09:25 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 09:25
Completed Parallel DNS resolution of 1 host. at 09:25, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 09:25
Scanning 10.10.11.229 [2 ports]
Discovered open port 22/tcp on 10.10.11.229
Discovered open port 80/tcp on 10.10.11.229
Completed Connect Scan at 09:25, 0.14s elapsed (2 total ports)
Initiating Service scan at 09:25
Scanning 2 services on 10.10.11.229
Completed Service scan at 09:25, 6.31s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.11.229.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 4.71s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.58s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
Nmap scan report for 10.10.11.229
Host is up, received user-set (0.14s latency).
Scanned at 2023-09-30 09:25:16 IST for 12s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 9.0p1 Ubuntu 1ubuntu7.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 9d:6e:ec:02:2d:0f:6a:38:60:c6:aa:ac:1e:e0:c2:84 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBP6mSkoF2+wARZhzEmi4RDFkpQx3gdzfggbgeI5qtcIseo7h1mcxH8UCPmw8Gx9+JsOjcNPBpHtp2deNZBzgKcA=
|   256 eb:95:11:c7:a6:fa:ad:74:ab:a2:c5:f6:a4:02:18:41 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOXXd7dM7wgVC+lrF0+ZIxKZlKdFhG2Caa9Uft/kLXDa
80/tcp open  http    syn-ack Apache httpd 2.4.54 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.54 (Ubuntu)
|_http-title: Zipping | Watch store
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 09:25
Completed NSE at 09:25, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.23 seconds
```
HTTP - TCP 80
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/93da4098-f408-41d9-a51a-10f23e80d0df)

File Upload
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b796d165-a542-485f-9d24-c1306171c082)
