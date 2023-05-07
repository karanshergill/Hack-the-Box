# Hack the Box - Lame

```CSS
Machine IP: 10.10.10.3 - Linux
Difficulty: Easy
Category: OSCP Preparation
```

# Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

## Port Scan
```CSS
▶ nmap -Pn -sS -p- 10.10.10.3 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.3
Host is up (0.18s latency).
Not shown: 65530 filtered tcp ports (no-response)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3632/tcp open  distccd

Nmap done: 1 IP address (1 host up) scanned in 131.61 seconds
```

## Service and Version Detection
```CSS
▶ nmap -sC -sV -p 21,22,139,445,3632 10.10.10.3 -oN services.nmap


```
