# Hack the Box - Support

```CSS
Machine IP: 10.10.11.174 - Windows
Difficulty: Easy
Category: OSCP Preparation
Vulnerabilities:
  - 
```

## Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

### Port Scan (TCP)
```CSS
▶ nmap -Pn -sS -O -p- 10.10.11.174 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.11.174
Host is up (0.17s latency).
Not shown: 65516 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49664/tcp open  unknown
49668/tcp open  unknown
49674/tcp open  unknown
49676/tcp open  unknown
49703/tcp open  unknown
57664/tcp open  unknown
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2016 (85%)
OS CPE: cpe:/o:microsoft:windows_server_2016
Aggressive OS guesses: Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 135.87 seconds
```
