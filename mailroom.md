# Hack the Box

## NMAP Scans
```CSS
▶ nmap -Pn -sS -T4 --min-rate 5000 -p- 10.10.11.209 -oN mailroom.surface                                           

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-22 01:12 IST
Nmap scan report for 10.10.11.209
Host is up (0.26s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 14.52 seconds
```

```CSS
▶ nmap -Pn -sC -sV -p 22,80 10.10.11.209 -oN mailroom.deep

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-22 01:16 IST
Nmap scan report for 10.10.11.209
Host is up (0.25s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 94:bb:2f:fc:ae:b9:b1:82:af:d7:89:81:1a:a7:6c:e5 (RSA)
|   256 82:1b:eb:75:8b:96:30:cf:94:6e:79:57:d9:dd:ec:a7 (ECDSA)
|_  256 19:fb:45:fe:b9:e4:27:5d:e5:bb:f3:54:97:dd:68:cf (ED25519)
80/tcp open  http    Apache httpd 2.4.54 ((Debian))
|_http-title: The Mail Room
|_http-server-header: Apache/2.4.54 (Debian)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.61 seconds
```

## HTTP
- Home
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d2d1e1bf-d68b-4eec-82ba-671144701bb8)

- Contact Us
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7c7c8a9c-e443-4322-9df5-d9f8dc3050cf)

## VHost
```CSS
▶ ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -H 'User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:15.0) Gecko/20100101 Firefox/15.0.1' -H 'Host: FUZZ.mailroom.htb' -u http://10.10.11.209 -fs 7748
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a51df4f4-8aee-4b12-b245-9e8df0efa8b2)

## Cross Site Scripting
- Contact Form
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/82186fed-786c-49a0-85c8-fcad35d89080)

- Cross Site Scripting in Contact Form
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ed23d09e-b6b4-43dd-92bd-0eb03cab0d00)

