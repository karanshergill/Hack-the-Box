# Hack the Box - Frolic

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.111 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.111
Host is up (0.18s latency).
Not shown: 65530 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
1880/tcp open  vsat-control
9999/tcp open  abyss
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/18%OT=22%CT=1%CU=42491%PV=Y%DS=2%DC=I%G=Y%TM=646608A
OS:8%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=104%TI=Z%CI=I%II=I%TS=8)SEQ
OS:(SP=105%GCD=1%ISR=104%TI=Z%CI=I%TS=8)OPS(O1=M53CST11NW7%O2=M53CST11NW7%O
OS:3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST11NW7%O6=M53CST11)WIN(W1=7120%W2=
OS:7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN(R=Y%DF=Y%T=40%W=7210%O=M53CNNSN
OS:W7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 81.36 seconds
```

```CSS
▶ nmap -sC -sV -p 22,139,445,1880,9999 10.10.10.111 -oN services.nmap

Nmap scan report for 10.10.10.111
Host is up (0.18s latency).          
                                          
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 877b912a0f11b6571ecb9f77cf35e221 (RSA)                                                                                                                            
|   256 b79b06ddc25e284478411e677d1eb762 (ECDSA)            
|_  256 21cf166d82a430c3c69cd738bab502b0 (ED25519)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
1880/tcp open  http        Node.js (Express middleware)
|_http-title: Node-RED
9999/tcp open  http        nginx 1.10.3 (Ubuntu)
|_http-server-header: nginx/1.10.3 (Ubuntu)
|_http-title: Welcome to nginx!
Service Info: Host: FROLIC; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -1h50m24s, deviation: 3h10m31s, median: -25s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-05-18T11:18:25
|_  start_date: N/A
|_nbstat: NetBIOS name: FROLIC, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: frolic
|   NetBIOS computer name: FROLIC\x00
|   Domain name: \x00
|   FQDN: frolic
|_  System time: 2023-05-18T16:48:25+05:30

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.59 seconds
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/e12b346f-5558-4210-b2b4-49c186a4ed0d)


![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/851dcf12-6391-47b1-b9ac-fcb42bdc725f)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/7af09321-c71e-47ce-b7f6-54b97ff4e6d8)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f1d15473-ffae-4dc0-a5d6-d270bf70a618)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a85d3683-a8a5-4a27-8361-694d4b252040)

```CSS
Credentials: admin:superduperlooperpassword_lol
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9240e526-17ab-45d1-8d1c-e68d93faad60)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/7591df2c-cc20-4b54-a986-4027d2568e1b)
