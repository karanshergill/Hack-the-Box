# Hack the Box - Swagshop
```CSS
Machine IP: 10.10.10.140 - Linux

Tags: magento
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.140 -T4 --min-rate 1000 -oN nmap.surface

Nmap scan report for 10.10.10.140
Host is up (0.20s latency).
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

```CSS
▶ nmap -sC -sV -p 22,80 10.10.10.140 -oN nmap.deep

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 b6552bd24e8fa3817261379a12f624ec (RSA)
|   256 2e30007a92f0893059c17756ad51c0ba (ECDSA)
|_  256 4c50d5f270c5fdc4b2f0bc4220326434 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Did not follow redirect to http://swagshop.htb/
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

## HTTP
![image](https://user-images.githubusercontent.com/83878909/230385940-576fb9d4-0154-4a75-af4c-ffeae45b4231.png)


## Magento
- Tool: [magescan](https://github.com/steverobbins/magescan)
```CSS
▶ magescan.phar scan:all http://swagshop.htb
```
- Magento Version Information
![image](https://user-images.githubusercontent.com/83878909/230405839-266cdc0e-97b7-4b08-bd5a-0b2afc29502f.png)
