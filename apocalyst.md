# Hack the Box - Apocalyst

```CSS
Machine IP: 10.10.10.46
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.46 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.46
Host is up (0.19s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```
```CSS
▶ nmap -sV -sC -p 22,80 10.10.10.46 -oN deep.nmap

Nmap scan report for 10.10.10.46
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 fdab0fc922d5f48f7a0a2911b404dac9 (RSA)
|   256 7692390a57bdf0032678c7db1a66a5bc (ECDSA)
|_  256 1212cff17fbe431fd5e66d908425c8bd (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apocalypse Preparation Blog
|_http-generator: WordPress 4.8
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.18 seconds
```

---

## HTTP
![image](https://user-images.githubusercontent.com/83878909/234799547-1b6562ae-e097-4a3a-9754-2e248dd220c4.png)

```CSS
echo "10.10.10.46 apocalyst.htb" >> /etc/hosts
```

![image](https://user-images.githubusercontent.com/83878909/234800289-380fc0b7-bc5b-4345-85f8-9bccb4587432.png)

![image](https://user-images.githubusercontent.com/83878909/234801910-0504a32c-a82c-42f7-9d3a-6bf60cd08204.png)

---

## WordPress
  - WPScan
```CSS
▶ wpscan --url http://apocalyst.htb --enumerate vt,tt,u,ap
```


## Content Discovery
  - Gobuster
```CSS
▶ gobuster dir -u http://apocalyst.htb -w /seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --add-slash --threads 50 --exclude-length 157
```

### Custom Wordlist
```CSS
▶ cewl http://apocalyst.htb -w apocalyst.lst
```
