# Hack the Box - Socket
```CSS
Machine IP: 10.10.11.206
```

## Reconnaissance
```CSS
▶ nmap -Pn -sS -p- 10.10.11.206 -T4 --min-rate 1000 -oN nmap.surface

Nmap scan report for 10.10.11.206
Host is up (0.18s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
5789/tcp open  unknown
```

```CSS
▶ nmap -sV -sC -p 22,80,5789 10.10.11.206 -oN nmap.deep

Nmap scan report for 10.10.11.206                                                     
Host is up (0.081s latency).                                                     
PORT     STATE SERVICE VERSION                                                        
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:                                                                        
|   256 4fe3a667a227f9118dc30ed773a02c28 (ECDSA)                          
|_  256 816e78766b8aea7d1babd436b7f8ecc4 (ED25519)                        
80/tcp   open  http    Apache httpd 2.4.52                                            
|_http-title: Did not follow redirect to http://qreader.htb/              
|_http-server-header: Apache/2.4.52 (Ubuntu)                              
5789/tcp open  unknown                                                                
| fingerprint-strings:                                                                
|   GenericLines, GetRequest, HTTPOptions, RTSPRequest:                   
|     HTTP/1.1 400 Bad Request                                                        
|     Date: Tue, 04 Apr 2023 06:08:33 GMT                                             
|     Server: Python/3.10 websockets/10.4                                             
|     Content-Length: 77                                                              
|     Content-Type: text/plain                                                        
|     Connection: close                                                               
|     Failed to open a WebSocket connection: did not receive a valid HTTP request.
|   Help, SSLSessionReq:                                                              
|     HTTP/1.1 400 Bad Request     
|     Date: Tue, 04 Apr 2023 06:08:49 GMT                                             
|     Server: Python/3.10 websockets/10.4
|     Content-Length: 77                                                                                                                                                    
|     Content-Type: text/plain                                                                                                                                              
|     Connection: close                                                                                                                                                     
|_    Failed to open a WebSocket connection: did not receive a valid HTTP request.
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port5789-TCP:V=7.93%I=7%D=4/4%Time=642BBEDA%P=x86_64-pc-linux-gnu%r(Gen
SF:ericLines,F4,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nDate:\x20Tue,\x2004
SF:\x20Apr\x202023\x2006:08:33\x20GMT\r\nServer:\x20Python/3\.10\x20websoc
SF:kets/10\.4\r\nContent-Length:\x2077\r\nContent-Type:\x20text/plain\r\nC
SF:onnection:\x20close\r\n\r\nFailed\x20to\x20open\x20a\x20WebSocket\x20co
SF:nnection:\x20did\x20not\x20receive\x20a\x20valid\x20HTTP\x20request\.\n
SF:")%r(GetRequest,F4,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nDate:\x20Tue,
SF:\x2004\x20Apr\x202023\x2006:08:33\x20GMT\r\nServer:\x20Python/3\.10\x20
SF:websockets/10\.4\r\nContent-Length:\x2077\r\nContent-Type:\x20text/plai
SF:n\r\nConnection:\x20close\r\n\r\nFailed\x20to\x20open\x20a\x20WebSocket
SF:\x20connection:\x20did\x20not\x20receive\x20a\x20valid\x20HTTP\x20reque
SF:st\.\n")%r(HTTPOptions,F4,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nDate:\
SF:x20Tue,\x2004\x20Apr\x202023\x2006:08:33\x20GMT\r\nServer:\x20Python/3\
SF:.10\x20websockets/10\.4\r\nContent-Length:\x2077\r\nContent-Type:\x20te
SF:xt/plain\r\nConnection:\x20close\r\n\r\nFailed\x20to\x20open\x20a\x20We
SF:bSocket\x20connection:\x20did\x20not\x20receive\x20a\x20valid\x20HTTP\x
SF:20request\.\n")%r(RTSPRequest,F4,"HTTP/1\.1\x20400\x20Bad\x20Request\r\
SF:nDate:\x20Tue,\x2004\x20Apr\x202023\x2006:08:33\x20GMT\r\nServer:\x20Py
SF:thon/3\.10\x20websockets/10\.4\r\nContent-Length:\x2077\r\nContent-Type
SF::\x20text/plain\r\nConnection:\x20close\r\n\r\nFailed\x20to\x20open\x20
SF:a\x20WebSocket\x20connection:\x20did\x20not\x20receive\x20a\x20valid\x2
SF:0HTTP\x20request\.\n")%r(Help,F4,"HTTP/1\.1\x20400\x20Bad\x20Request\r\
SF:nDate:\x20Tue,\x2004\x20Apr\x202023\x2006:08:49\x20GMT\r\nServer:\x20Py
SF:thon/3\.10\x20websockets/10\.4\r\nContent-Length:\x2077\r\nContent-Type
SF::\x20text/plain\r\nConnection:\x20close\r\n\r\nFailed\x20to\x20open\x20
SF:a\x20WebSocket\x20connection:\x20did\x20not\x20receive\x20a\x20valid\x2
SF:0HTTP\x20request\.\n")%r(SSLSessionReq,F4,"HTTP/1\.1\x20400\x20Bad\x20R
SF:equest\r\nDate:\x20Tue,\x2004\x20Apr\x202023\x2006:08:49\x20GMT\r\nServ
SF:er:\x20Python/3\.10\x20websockets/10\.4\r\nContent-Length:\x2077\r\nCon
SF:tent-Type:\x20text/plain\r\nConnection:\x20close\r\n\r\nFailed\x20to\x2
SF:0open\x20a\x20WebSocket\x20connection:\x20did\x20not\x20receive\x20a\x2
SF:0valid\x20HTTP\x20request\.\n");
Service Info: Host: qreader.htb; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
## Port 80 (HTTP)
![image](https://user-images.githubusercontent.com/83878909/229703936-7e17a816-81bd-423d-85d0-87340533cdc2.png)

## Port 5789 (Web Socket)
- Test websocket for vulnerabilities.
- Tool: [STEWS](https://github.com/PalindromeLabs/STEWS)
- Test for generic Cross-site WebSocket Hijacking (CSWSH).

```CSS
▶ python3 STEWS-vuln-detect.py -1 -n -u 10.10.11.206:5789

Testing ws://10.10.11.206:5789
>>>Note: ws://10.10.11.206:5789 allowed http or https for origin
>>>Note: ws://10.10.11.206:5789 allowed null origin
>>>Note: ws://10.10.11.206:5789 allowed unusual char (possible parse error)
>>>VANILLA CSWSH DETECTED: ws://10.10.11.206:5789 likely vulnerable to vanilla CSWSH (any origin)
====Full list of vulnerable URLs===
['ws://10.10.11.206:5789']
['>>>VANILLA CSWSH DETECTED: ws://10.10.11.206:5789 likely vulnerable to vanilla CSWSH (any origin)']
```
![image](https://user-images.githubusercontent.com/83878909/229711076-b95bf50d-7021-4e24-8d5a-8d28cb23c0a1.png)

## Application
- The website offers functions to generate and scan a QR code both online and offline.
![image](https://user-images.githubusercontent.com/83878909/229722201-95ca3832-3091-42b6-ab72-70edc0d413fe.png)

- Download the Windows version and decompile the `.exe` file.
- Tool: [pyinstxtractor](https://github.com/extremecoders-re/pyinstxtractor)
![image](https://user-images.githubusercontent.com/83878909/229724067-57f3db4f-3de5-4057-b3c1-c4a9c74a9fd8.png)
![image](https://user-images.githubusercontent.com/83878909/229725104-5a4320b4-2d0a-4033-9924-908951d05a2c.png)

