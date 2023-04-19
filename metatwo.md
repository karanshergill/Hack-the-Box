# Hack the Box - MetaTwo

```CSS
IP: 10.10.11.186 - Linux
CMS: WordPress
```

## Open TCP Ports
### NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.11.186 -T4 --max-rate 1000 -oN open-ports.nmap

Nmap scan report for 10.10.11.186
Host is up (0.18s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh                                                                     
80/tcp open  http                                                                                                                                                          
                                                                                     
Nmap done: 1 IP address (1 host up) scanned in 608.38 seconds
```

## Open TCP Ports - Enumeration
### NMAP
```CSS
▶ nmap -sC -sV -p 21,22,80 10.10.11.186 -oN enum-ports.nmap

Nmap scan report for 10.10.11.186
Host is up (0.18s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh                                                                     
80/tcp open  http                                                                                                                                                          
                                                                                     
Nmap done: 1 IP address (1 host up) scanned in 608.38 seconds
➜  metatwo nmap -sC -sV -p 21,22,80 10.10.11.186 -oN enum-ports.nmap                  
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-19 13:13 IST
Nmap scan report for 10.10.11.186
Host is up (0.18s latency).
                                          
PORT   STATE SERVICE VERSION
21/tcp open  ftp?                                                                    
| fingerprint-strings:                                                               
|   GenericLines:                                                                    
|     220 ProFTPD Server (Debian) [::ffff:10.10.11.186]           
|     Invalid command: try being more creative
|_    Invalid command: try being more creative 
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey:                                                                       
|   3072 c4b44617d2102d8fec1dc927fecd79ee (RSA)
|   256 2aea2fcb23e8c529409cab866dcd4411 (ECDSA)
|_  256 fd78c0b0e22016fa050debd83f12a4ab (ED25519)            
80/tcp open  http    nginx 1.18.0                                                                                                                                          |_http-server-header: nginx/1.18.0
|_http-title: Did not follow redirect to http://metapress.htb/            
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service 
:                                                                                    
SF-Port21-TCP:V=7.93%I=7%D=4/19%Time=643F9BA1%P=x86_64-pc-linux-gnu%r(Gene
SF:ricLines,8F,"220\x20ProFTPD\x20Server\x20\(Debian\)\x20\[::ffff:10\.10\
SF:.11\.186\]\r\n500\x20Invalid\x20command:\x20try\x20being\x20more\x20cre
SF:ative\r\n500\x20Invalid\x20command:\x20try\x20being\x20more\x20creative
SF:\r\n");                                                                                                                                                                 
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel      
                                                                                                                                                                           
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 214.25 seconds
```

---

## WebServer
### Homepage
![image](https://user-images.githubusercontent.com/83878909/233007255-a55cb9c3-366e-4829-a1f8-9638da827959.png)
### Events
![image](https://user-images.githubusercontent.com/83878909/233008739-59e1f807-2a3d-4aa3-8330-d1f533cc569b.png)

---

## Content Discovery
### Brute-force Common Directories and Files
```CSS
▶ ffuf -u http://metapress.htb/FUZZ -w /usr/share/wordlists/ctf/common.txt:FUZZ -mc 200 -o directory.fuzz
```
![image](https://user-images.githubusercontent.com/83878909/233014753-408a5dd1-fb01-4d53-841b-b3104fbe05da.png)
