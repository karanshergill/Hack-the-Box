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

