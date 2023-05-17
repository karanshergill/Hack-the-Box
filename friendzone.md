# Hack the Box - FriendZone

```CSS
Machine IP: 10.10.10.123
```

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.123 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.123
Host is up (0.15s latency).
Not shown: 65528 closed tcp ports (reset)
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
53/tcp  open  domain
80/tcp  open  http
139/tcp open  netbios-ssn
443/tcp open  https
445/tcp open  microsoft-ds
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/17%OT=21%CT=1%CU=37156%PV=Y%DS=2%DC=I%G=Y%TM=64647D0
OS:8%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=10B%TI=Z%CI=I%II=I%TS=A)OPS
OS:(O1=M53CST11NW7%O2=M53CST11NW7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST1
OS:1NW7%O6=M53CST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN
OS:(R=Y%DF=Y%T=40%W=7210%O=M53CNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 81.47 seconds
```

```CSS
▶ nmap -sC -sV -p 21,22,53,80,139,443,445 10.10.10.123 -oN service.nmap

Nmap scan report for 10.10.10.123
Host is up (0.18s latency).      
                                                                                     
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 3.0.3  
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:                           
|   2048 a96824bc971f1e54a58045e74cd9aaa0 (RSA)
|   256 e5440146ee7abb7ce91acb14999e2b8e (ECDSA)
|_  256 004e1a4f33e8a0de86a6e42a5f84612b (ED25519)
53/tcp  open  domain      ISC BIND 9.11.3-1ubuntu1.2 (Ubuntu Linux)                                                                                                        
| dns-nsid: 
|_  bind.version: 9.11.3-1ubuntu1.2-Ubuntu                                                                                                                                 
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))    
|_http-title: Friend Zone Escape software
|_http-server-header: Apache/2.4.29 (Ubuntu)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
443/tcp open  ssl/http    Apache httpd 2.4.29
| ssl-cert: Subject: commonName=friendzone.red/organizationName=CODERED/stateOrProvinceName=CODERED/countryName=JO
| Not valid before: 2018-10-05T21:02:30
|_Not valid after:  2018-11-04T21:02:30
|_http-server-header: Apache/2.4.29 (Ubuntu)
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
|_http-title: 404 Not Found
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
Service Info: Hosts: FRIENDZONE, 127.0.1.1; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -1h00m24s, deviation: 1h43m54s, median: -25s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-05-17T07:27:35
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: friendzone
|   NetBIOS computer name: FRIENDZONE\x00
|   Domain name: \x00
|   FQDN: friendzone
|_  System time: 2023-05-17T10:27:36+03:00
|_nbstat: NetBIOS name: FRIENDZONE, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.82 seconds
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/06dd652f-5623-439c-9c9c-2a439e9e183e)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/e4616dad-d202-41c4-a7b4-31b961b2ef76)

Hostname Disclosure
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/cf335497-84cf-4db5-8478-f16d624e3baf)
```CSS
▶ nslookup friendzoneportal.red 10.10.10.123
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/b2ff9349-a5d3-4348-822e-d68b949fb424)

Zone Transfer
```CSS
▶ dig axfr @10.10.10.123 friendzone.red
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d245a5c6-8d45-4d14-ab87-f56c50334d73)

```CSS
▶ dig axfr @10.10.10.123 friendzoneportal.red
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d76122e3-d1b7-41db-b042-16fd11951483)

Virtual Hosts
```CSS
administrator1.friendzone.red
hr.friendzone.red
uploads.friendzone.red
admin.friendzoneportal.red
files.friendzoneportal.red
imports.friendzoneportal.red
vpn.friendzoneportal.red
```

SMB
```CSS
▶ smbmap -H 10.10.10.123 
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/318b883a-f244-4562-a1a4-b145ca77efe7)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2d3fa62f-789e-4b37-9ce2-dc0fe0e355f7)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/10d3cfd7-4f8a-4ad4-bbd2-d75935e016ea)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/5672e92e-431e-4765-b445-a685a3341601)
```CSS
admin:WORKWORKHhallelujah@#
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/15569cf5-0257-45fd-ab1c-fe7cddcaf121)

