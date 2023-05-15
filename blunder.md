# Hack the Box - Blunder

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.191 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.191
Host is up (0.19s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE  SERVICE
21/tcp closed ftp
80/tcp open   http
Device type: general purpose|storage-misc|WAP
Running (JUST GUESSING): Linux 5.X|4.X|2.6.X|3.X (98%), HP embedded (91%), Ubiquiti AirOS 5.X (89%), Ubiquiti embedded (89%)
OS CPE: cpe:/o:linux:linux_kernel:5.0 cpe:/h:hp:p2000_g3 cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:2.6.32 cpe:/o:linux:linux_kernel:3 cpe:/o:ubnt:airos:5.2.6 cpe:/h:ubnt:airmax_nanostation
Aggressive OS guesses: Linux 5.0 (98%), Linux 5.4 (93%), Linux 5.0 - 5.4 (93%), HP P2000 G3 NAS device (91%), Linux 4.15 - 5.6 (91%), Linux 5.3 - 5.4 (90%), Linux 2.6.32 (90%), Linux 2.6.32 - 3.1 (90%), Linux 5.1 (90%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (89%)
No exact OS matches for host (test conditions non-ideal).

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 134.49 seconds
```

```CSS
▶ nmap -sC -sV -p 21,80 10.10.10.191 -oN services.nmap

Nmap scan report for 10.10.10.191
Host is up (0.18s latency).

PORT   STATE  SERVICE VERSION
21/tcp closed ftp
80/tcp open   http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-generator: Blunder
|_http-title: Blunder | A blunder of interesting facts

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.23 seconds
```

---

## HTTP 80
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f70628d0-2b79-45bb-af4e-e683b063aa20)

---

## Content Discovery

```CSS
▶ gobuster dir --url http://10.10.10.191 --wordlist /usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt --threads 20
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4075b582-c7ff-44a4-8767-fe978f218cc9)

```CSS
▶ gobuster dir --url http://10.10.10.191 --wordlist /usr/share/seclists/Discovery/Web-Content/raft-large-files.txt --threads 20
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c1979746-2805-426a-9824-c5f46d09a09b)


---
