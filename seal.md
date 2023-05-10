# Hack the Box - Seal

```CSS
Machine IP: 10.10.10.250 - Linux
Difficulty: Medium
Category: OSCP Preparation
```

# Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

## Port Scan (TCP)
```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.250 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.250
Host is up (0.17s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
443/tcp  open  https
8080/tcp open  http-proxy
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/10%OT=22%CT=1%CU=31966%PV=Y%DS=2%DC=I%G=Y%TM=645BC96
OS:2%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=10A%TI=Z%CI=Z%II=I%TS=A)OPS
OS:(O1=M53CST11NW7%O2=M53CST11NW7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST1
OS:1NW7%O6=M53CST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN
OS:(R=Y%DF=Y%T=40%W=FAF0%O=M53CNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 93.26 seconds
```

## Service and Version Detection
```CSS
▶ nmap -sC -sV -p 22,43,8080 10.10.10.250 -oN services.nmap

Nmap scan report for 10.10.10.250                                                    
Host is up (0.17s latency).                                                          
                                                                                     
PORT     STATE  SERVICE    VERSION                                                   
22/tcp   open   ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:                                                                       
|   3072 4b894739673d07315e3f4c27411ff967 (RSA)                                      
|   256 04a74f399565c5b08dd5492ed8440036 (ECDSA)                          
|_  256 b45e8393c54249de7125927123b18554 (ED25519)                                   
43/tcp   closed whois                                                                
8080/tcp open   http-proxy                                                           
|_http-title: Site doesn't have a title (text/html;charset=utf-8).                   
| http-auth:                                                                         
| HTTP/1.1 401 Unauthorized\x0D                                                      
|_  Server returned status 401 but no WWW-Authenticate header.                       
| fingerprint-strings:
|   FourOhFourRequest:                                                               
|     HTTP/1.1 401 Unauthorized
|     Date: Wed, 10 May 2023 16:45:21 GMT                                                                                                                                 
|     Set-Cookie: JSESSIONID=node04mlz2fwh9s4j119zpsysuahz32.node0; Path=/; HttpOnly
|     Expires: Thu, 01 Jan 1970 00:00:00 GMT
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 0
|   GetRequest: 
|     HTTP/1.1 401 Unauthorized
|     Date: Wed, 10 May 2023 16:45:19 GMT
|     Set-Cookie: JSESSIONID=node01rozln8ivln9dyfyvnqefnxwz0.node0; Path=/; HttpOnly
|     Expires: Thu, 01 Jan 1970 00:00:00 GMT
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 0
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Date: Wed, 10 May 2023 16:45:20 GMT
|     Set-Cookie: JSESSIONID=node07vji2je08bptb0xv5r688l1m1.node0; Path=/; HttpOnly
|     Expires: Thu, 01 Jan 1970 00:00:00 GMT
|     Content-Type: text/html;charset=utf-8
|     Allow: GET,HEAD,POST,OPTIONS
|     Content-Length: 0
|   RPCCheck: 
|     HTTP/1.1 400 Illegal character OTEXT=0x80
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 71
|     Connection: close
|     <h1>Bad Message 400</h1><pre>reason: Illegal character OTEXT=0x80</pre>
|   RTSPRequest: 
|     HTTP/1.1 505 Unknown Version                                                                                                                                        
|     Content-Type: text/html;charset=iso-8859-1                                                                                                                          
|     Content-Length: 58                                                                                                                                                  
|     Connection: close                                                                                                                                                   
|     <h1>Bad Message 505</h1><pre>reason: Unknown Version</pre>
|   Socks4: 
|     HTTP/1.1 400 Illegal character CNTL=0x4
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 69
|     Connection: close
|     <h1>Bad Message 400</h1><pre>reason: Illegal character CNTL=0x4</pre>
|   Socks5: 
|     HTTP/1.1 400 Illegal character CNTL=0x5
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 69
|     Connection: close
|_    <h1>Bad Message 400</h1><pre>reason: Illegal character CNTL=0x5</pre>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service
 :
SF-Port8080-TCP:V=7.93%I=7%D=5/10%Time=645BCA37%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,F4,"HTTP/1\.1\x20401\x20Unauthorized\r\nDate:\x20Wed,\x2010\x2
SF:0May\x202023\x2016:45:19\x20GMT\r\nSet-Cookie:\x20JSESSIONID=node01rozl
SF:n8ivln9dyfyvnqefnxwz0\.node0;\x20Path=/;\x20HttpOnly\r\nExpires:\x20Thu
SF:,\x2001\x20Jan\x201970\x2000:00:00\x20GMT\r\nContent-Type:\x20text/html
SF:;charset=utf-8\r\nContent-Length:\x200\r\n\r\n")%r(HTTPOptions,107,"HTT
SF:P/1\.1\x20200\x20OK\r\nDate:\x20Wed,\x2010\x20May\x202023\x2016:45:20\x
SF:20GMT\r\nSet-Cookie:\x20JSESSIONID=node07vji2je08bptb0xv5r688l1m1\.node
SF:0;\x20Path=/;\x20HttpOnly\r\nExpires:\x20Thu,\x2001\x20Jan\x201970\x200
SF:0:00:00\x20GMT\r\nContent-Type:\x20text/html;charset=utf-8\r\nAllow:\x2
SF:0GET,HEAD,POST,OPTIONS\r\nContent-Length:\x200\r\n\r\n")%r(RTSPRequest,
SF:AD,"HTTP/1\.1\x20505\x20Unknown\x20Version\r\nContent-Type:\x20text/htm
SF:l;charset=iso-8859-1\r\nContent-Length:\x2058\r\nConnection:\x20close\r
SF:\n\r\n<h1>Bad\x20Message\x20505</h1><pre>reason:\x20Unknown\x20Version<
SF:/pre>")%r(FourOhFourRequest,F4,"HTTP/1\.1\x20401\x20Unauthorized\r\nDat
SF:e:\x20Wed,\x2010\x20May\x202023\x2016:45:21\x20GMT\r\nSet-Cookie:\x20JS
SF:ESSIONID=node04mlz2fwh9s4j119zpsysuahz32\.node0;\x20Path=/;\x20HttpOnly
SF:\r\nExpires:\x20Thu,\x2001\x20Jan\x201970\x2000:00:00\x20GMT\r\nContent
SF:-Type:\x20text/html;charset=utf-8\r\nContent-Length:\x200\r\n\r\n")%r(S
SF:ocks5,C3,"HTTP/1\.1\x20400\x20Illegal\x20character\x20CNTL=0x5\r\nConte
SF:nt-Type:\x20text/html;charset=iso-8859-1\r\nContent-Length:\x2069\r\nCo
SF:nnection:\x20close\r\n\r\n<h1>Bad\x20Message\x20400</h1><pre>reason:\x2
SF:0Illegal\x20character\x20CNTL=0x5</pre>")%r(Socks4,C3,"HTTP/1\.1\x20400
SF:\x20Illegal\x20character\x20CNTL=0x4\r\nContent-Type:\x20text/html;char
SF:set=iso-8859-1\r\nContent-Length:\x2069\r\nConnection:\x20close\r\n\r\n
SF:<h1>Bad\x20Message\x20400</h1><pre>reason:\x20Illegal\x20character\x20C
SF:NTL=0x4</pre>")%r(RPCCheck,C7,"HTTP/1\.1\x20400\x20Illegal\x20character
SF:\x20OTEXT=0x80\r\nContent-Type:\x20text/html;charset=iso-8859-1\r\nCont
SF:ent-Length:\x2071\r\nConnection:\x20close\r\n\r\n<h1>Bad\x20Message\x20
SF:400</h1><pre>reason:\x20Illegal\x20character\x20OTEXT=0x80</pre>");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 41.80 seconds
```

---

# Enumeration
## Port 22 - SSH
  - The OpenSSH version that is running is not associated with any critical vulnerabilities, so it’s unlikely to gain initial access through this port, unless some valid credentials are found.

## Port 80 HTTP
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4ff70451-a9c1-4926-ae42-8bc7911217b0)

## Port 8080 HTTP Proxy
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/67431678-77dc-4620-80e9-211c14b6ce97)

---

# Content Discovery
  - Brute-force common directories and files.
```CSS
▶ gobuster dir --url https://10.10.10.250 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25 --no-tls-validation
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/79031ee3-0750-4358-9168-c143f1af023d)

```CSS
▶ gobuster dir --url https://10.10.10.250/admin --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25 --no-tls-validation
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a544a2ee-1518-480a-aa86-58c46c4780b0)

```CSS
▶ gobuster dir --url https://10.10.10.250/host-manager --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25 --no-tls-validation
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/76aff29e-a205-4b61-a672-4d3a4e38ad50)

```CSS
▶ gobuster dir --url https://10.10.10.250/manager --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25 --no-tls-validation
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/afd4b4d6-d29a-495d-bc6f-734ae67e3d2e)

---

# Git Bucket
  - Logging in with Git Bucket default credentials failed.
  - Git Bucket default credentials: `root:root`
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ceaddd26-18cb-4181-a557-fb557966d987)

  - Register a new account on Git Bucket.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/3291eb50-58eb-4360-abbb-95612af30e28)

  - Login with the account credentials.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/3299e3ed-1b97-49ff-a439-2cc01bdac7b8)

  - Read permission on two repositories. The infra repository reveals ansible templates to configure tomcat.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4bdb75a0-c92e-4bf3-bd5b-1a72c5b9a1d7)

  - Developer Comments.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a7dc4650-7d37-42ea-a77c-530f4cd55c0f)
