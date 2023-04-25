# Hack the Box - Vault

## NMAP
```CSS
▶ nmap -sS -Pn -p- 10.10.10.109 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.109
Host is up (0.18s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

```CSS
▶ nmap -sV -sC -p 22,80 10.10.10.109 -oN deep.nmap

Nmap scan report for 10.10.10.109
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 a69d0f7d7375bba8940ab7e3fe1f24f4 (RSA)
|   256 2c7c34eb3aeb0403ac48285409743d27 (ECDSA)
|_  256 98425fad8722926d72e6666c82c10983 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

## HTTP
![image](https://user-images.githubusercontent.com/83878909/234180522-bb09553f-542f-489d-97e8-6801fbcb6287.png)

## Content Discovery
```CSS
▶ ffuf -u http://10.10.10.109/sparklays/FUZZ.php -w directory-list-2.3-medium.txt
```
![image](https://user-images.githubusercontent.com/83878909/234184393-f4915ea3-9ec4-46f5-a818-4da6beb33aae.png)

  - `http://10.10.10.109/sparklays/admin.php`
![image](https://user-images.githubusercontent.com/83878909/234184649-5d3736d8-42b0-437b-8b86-b7e50f487e50.png)
  - `http://10.10.10.109/sparklays/login.php`
![image](https://user-images.githubusercontent.com/83878909/234184743-478cd40a-74f0-46ec-afc7-43f87e26a58e.png)

