# Hack the Box - Armageddon

# NMAP
```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.233 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.233
Host is up (0.18s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/15%OT=22%CT=1%CU=37173%PV=Y%DS=2%DC=I%G=Y%TM=6461351
OS:5%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=107%TI=Z%II=I%TS=A)SEQ(SP=1
OS:05%GCD=1%ISR=107%TI=Z%CI=I%II=I%TS=A)SEQ(SP=105%GCD=1%ISR=107%TI=Z%CI=I%
OS:TS=A)SEQ(SP=105%GCD=1%ISR=107%TI=Z%TS=A)OPS(O1=M53CST11NW7%O2=M53CST11NW
OS:7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST11NW7%O6=M53CST11)WIN(W1=7120%
OS:W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN(R=Y%DF=Y%T=40%W=7210%O=M53CN
OS:NSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=
OS:Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=A
OS:R%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=4
OS:0%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=
OS:G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 85.58 seconds
```

```CSS
▶ nmap -sC -sV -p 22,80 10.10.10.233 -oN services.nmap

Nmap scan report for 10.10.10.233
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 82c6bbc7026a93bb7ccbdd9c30937934 (RSA)
|   256 3aca9530f312d7ca4505bcc7f116bbfc (ECDSA)
|_  256 7ad4b36879cf628a7d5a61e7060f5f33 (ED25519)
80/tcp open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.4.16)
|_http-title: Welcome to  Armageddon |  Armageddon
|_http-generator: Drupal 7 (http://drupal.org)
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.4.16
| http-robots.txt: 36 disallowed entries (15 shown)
| /includes/ /misc/ /modules/ /profiles/ /scripts/ 
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt 
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt 
|_/LICENSE.txt /MAINTAINERS.txt

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.35 seconds
```

---

## HTTP
  - Homepage
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/cb5ace1e-fa12-4cc5-b837-4107afa14893)

  - Registering as a new user failed as e-mail authentication is broken broken.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9a5aaa2b-0ce1-4ec1-b1f4-cab73c395c9f)

---

## Exploit
  - The Drupal version running is vulnerable to Remote Code Execution - CVE-2018-7600
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/996b2dd6-a19d-4ae4-bcf2-ff0c9057302e)

  
  - Drupal exploit is not working.
