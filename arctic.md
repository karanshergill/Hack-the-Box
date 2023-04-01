# Hack the Box - Arctic

```CSS
Machine IP: 10.10.10.11 - Windows
```

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

