# HTB - Beep

## NMAP
```CSS
▶ nmap -Pn -sS -T4 --min-rate 5000 -p- 10.10.10.7

Nmap scan report for 10.10.10.7
Host is up (0.29s latency).
Not shown: 65519 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh 
25/tcp    open  smtp
80/tcp    open  http   
110/tcp   open  pop3
111/tcp   open  rpcbind
143/tcp   open  imap   
443/tcp   open  https
878/tcp   open  unknown
993/tcp   open  imaps
995/tcp   open  pop3s
3306/tcp  open  mysql    
4190/tcp  open  sieve  
4445/tcp  open  upnotifyp
4559/tcp  open  hylafax         
5038/tcp  open  unknown
10000/tcp open  snet-sensor-mgmt

Nmap done: 1 IP address (1 host up) scanned in 19.06 seconds
```

```CSS
▶ nmap -Pn -sC -sV -T4 --min-rate 5000 -p 22,25,80,110,111,143,443,878,993,995,3306,4190,4445,4459,5038,10000 10.10.10.7

Nmap scan report for 10.10.10.7                                                                                                                                            
Host is up (0.26s latency).                                                                                                                                                
                                                                                                                                                                           
PORT      STATE  SERVICE    VERSION                                                                                                                                        
22/tcp    open   ssh        OpenSSH 4.3 (protocol 2.0)                                                                                                                     
| ssh-hostkey:                                                                                                                                                             
|   1024 ad:ee:5a:bb:69:37:fb:27:af:b8:30:72:a0:f9:6f:53 (DSA)                                                                                                             
|_  2048 bc:c6:73:59:13:a1:8a:4b:55:07:50:f6:65:1d:6d:0d (RSA)                                                                                                             
25/tcp    open   smtp       Postfix smtpd                                                                                                                                  
|_smtp-commands: beep.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, ENHANCEDSTATUSCODES, 8BITMIME, DSN                                                               
80/tcp    open   http       Apache httpd 2.2.3
|_http-server-header: Apache/2.2.3 (CentOS)
|_http-title: Did not follow redirect to https://10.10.10.7/
110/tcp   open   pop3       Cyrus pop3d 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
|_pop3-capabilities: LOGIN-DELAY(0) APOP EXPIRE(NEVER) IMPLEMENTATION(Cyrus POP3 server v2) STLS PIPELINING USER UIDL RESP-CODES AUTH-RESP-CODE TOP
111/tcp   open   rpcbind    2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service 
|   100000  2            111/tcp   rpcbind 
|   100000  2            111/udp   rpcbind 
|   100024  1            875/udp   status
|_  100024  1            878/tcp   status
143/tcp   open   imap       Cyrus imapd 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
|_imap-capabilities: THREAD=REFERENCES Completed OK UIDPLUS SORT=MODSEQ URLAUTHA0001 CONDSTORE NO ID RENAME ATOMIC RIGHTS=kxte CATENATE LIST-SUBSCRIBED BINARY QUOTA LISTEXT IDLE ANNOTATEMORE THREAD=ORDEREDSUBJECT SORT MAILBOX-REFERRALS X-NETSCAPE NAMESPACE CHILDREN MULTIAPPEND STARTTLS ACL UNSELECT IMAP4 LITERAL+ IMAP4rev1
443/tcp   open   ssl/http   Apache httpd 2.2.3 ((CentOS))
|_http-server-header: Apache/2.2.3 (CentOS)
| http-robots.txt: 1 disallowed entry 
|_/
|_ssl-date: 2023-08-11T07:49:19+00:00; +1s from scanner time.
|_http-title: Elastix - Login page
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2017-04-07T08:22:08
|_Not valid after:  2018-04-07T08:22:08
878/tcp   open   status     1 (RPC #100024)
993/tcp   open   ssl/imap   Cyrus imapd
|_imap-capabilities: CAPABILITY
995/tcp   open   pop3       Cyrus pop3d
3306/tcp  open   mysql      MySQL (unauthorized)
4190/tcp  open   sieve      Cyrus timsieved 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4 (included w/cyrus imap)
4445/tcp  open   upnotifyp?
4459/tcp  closed unknown
5038/tcp  open   asterisk   Asterisk Call Manager 1.1
10000/tcp open   http       MiniServ 1.570 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
Service Info: Hosts:  beep.localdomain, 127.0.0.1, example.com

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 400.11 seconds
```

## HTTP
- Elastix Login Page
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5150d735-7a74-4f0d-b6d6-cfe7d5ef5fe9)

## Content Discovery
- Brute-force directories and files
```CSS
▶ gobuster dir --url https://10.10.10.7 --extensions php --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt --threads 10 --no-tls-validation
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/281c923c-e137-4866-9dd6-986ad724abd2)

## Search Exploit
```CSS
▶ searchsploit elastix
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d5e7a3be-8a35-4934-8e0e-3c54643cfede)
```CSS
▶ searchsploit -x php/webapps/37637.pl
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a0e55005-02c0-4e54-800c-c5378e2603cc)

# Elastix 2.2.0 (VTiger CRM) Exploit - LFI
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/1c2e07d9-5241-4df4-a0e5-761a5a603cd5)
- Password found: jEhdIekWmdjE

# SSH Login
- SSH as root
```CSS
▶ ssh root@10.10.10.7
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8598d677-48df-4c24-9128-cf1380f14271)

## SSH Depricated Ciphers Fix
- Add the below lines to
```CSS
Ciphers 3des-cbc,aes128-cbc,aes192-cbc,aes256-cbc,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com,chacha20-poly1305@openssh.com
MACs hmac-sha1,hmac-sha1-96,hmac-sha2-256,hmac-sha2-512,hmac-md5,hmac-md5-96,umac-64@openssh.com,umac-128@openssh.com,hmac-sha1-etm@openssh.com,hmac-sha1-96-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-md5-etm@openssh.com,hmac-md5-96-etm@openssh.com,umac-64-etm@openssh.com,umac-128-etm@openssh.com
HostKeyAlgorithms ssh-ed25519,ssh-ed25519-cert-v01@openssh.com,sk-ssh-ed25519@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,ssh-rsa,ssh-dss,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com,ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com
KexAlgorithms diffie-hellman-group1-sha1,diffie-hellman-group14-sha1,diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group-exchange-sha1,diffie-hellman-group-exchange-sha256,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,curve25519-sha256,curve25519-sha256@libssh.org,sntrup761x25519-sha512@openssh.com
```
