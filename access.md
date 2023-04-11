# Hack the Box - Access

```CSS
Machine IP: 10.10.10.98
```

- [NMAP: All TCP ports](#nmap)
- [NMAP: Open ports Service Version](#nmap-service-version)
- [FTP Anonymous Login](#ftp-login)

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

## FTP Login
