# Hack the Box - Admirer

```CSS
Machine IP: 10.10.10.187 - Linux
```

# Reconaissance
## NMAP (Surface)
```CSS
▶ nmap -Pn -sS -p- 10.10.10.187 -T4 --min-rate 1000 -oN nmap.surface

Nmap scan report for 10.10.10.187
Host is up (0.100s latency).
Not shown: 65532 closed tcp ports (reset)

PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 75.35 seconds
```

## NMAP (Deep)
```CSS
▶ nmap -sC -sV -p 21,22,80 10.10.10.187 -oN nmap.deep

Nmap scan report for 10.10.10.187
Host is up (0.088s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.4p1 Debian 10+deb9u7 (protocol 2.0)
| ssh-hostkey: 
|   2048 4a71e92163699dcbdd84021a2397e1b9 (RSA)
|   256 c595b6214d46a425557a873e19a8e702 (ECDSA)
|_  256 d02dddd05c42f87b315abe57c4a9a756 (ED25519)
80/tcp open  http    Apache httpd 2.4.25 ((Debian))
| http-robots.txt: 1 disallowed entry 
|_/admin-dir
|_http-title: Admirer
|_http-server-header: Apache/2.4.25 (Debian)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.59 seconds
```

## Application (Port 80)
![image](https://user-images.githubusercontent.com/83878909/229423143-85c36971-4509-41d0-8710-63c5cf8efe6e.png)
