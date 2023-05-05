# Hack the Box - Bart

```CSS
Machine IP: 10.10.10.63 - Windows
Difficulty: Medium
Category: OSCP Preparation
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.81 -T4 --min-rate 1000 -oN bart-ports.nmap

Nmap scan report for 10.10.10.81
Host is up (0.19s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http
```

```CSS
▶ nmap -sC -sV -p 80 10.10.10.81 -oN bart-services.nmap

Nmap scan report for 10.10.10.81
Host is up (0.20s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Did not follow redirect to http://forum.bart.htb/
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.48 seconds
```

---

