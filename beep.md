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
