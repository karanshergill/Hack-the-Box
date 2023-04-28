# Hack The Box - Optimum

```CSS
Machine IP: 10.10.10.8
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.8 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.8
Host is up (0.18s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http

▶ nmap -sC -sV -p 80 10.10.10.8 -oN deep.nmap

Nmap scan report for 10.10.10.8
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    HttpFileServer httpd 2.3
|_http-server-header: HFS 2.3
|_http-title: HFS /
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

