# Hack the Box - Doctor

```CSS 
Machine IP: 10.10.10.209
```

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.209 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.209
Host is up (0.21s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8089/tcp open  unknown
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 5.0 (97%), Linux 4.15 - 5.6 (92%), Linux 5.4 (90%), Crestron XPanel control system (90%), Linux 5.3 - 5.4 (90%), Linux 5.0 - 5.3 (89%), Linux 5.0 - 5.4 (88%), Linux 2.6.32 (88%), ASUS RT-N56U WAP (Linux 3.4) (87%), Linux 3.1 (87%)
No exact OS matches for host (test conditions non-ideal).

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 138.10 seconds
```

```CSS
▶ nmap -sC -sV -p 22,80,8089 10.10.10.209 -oN services.nmap

Nmap scan report for 10.10.10.209
Host is up (0.18s latency).

PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 594d4ec2d8cfda9da8c8d0fd99a84617 (RSA)
|   256 7ff3dcfb2dafcbff9934ace0f8001e47 (ECDSA)
|_  256 530e966b9ce9c1a170516c2dce7b43e8 (ED25519)
80/tcp   open  http     Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Doctor
8089/tcp open  ssl/http Splunkd httpd
| ssl-cert: Subject: commonName=SplunkServerDefaultCert/organizationName=SplunkUser
| Not valid before: 2020-09-06T15:57:27
|_Not valid after:  2023-09-06T15:57:27
|_http-title: splunkd
|_http-server-header: Splunkd
| http-robots.txt: 1 disallowed entry 
|_/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 46.01 seconds
```
## HTTP 80
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4fdf842b-3b62-46fd-8ce2-de8b1d5aec36)

## Virtual Host
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/975f588d-00eb-445d-86b5-6d5329c73a4a)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c4ff87b3-8fb5-4997-b54e-73d290e0cbf5)
