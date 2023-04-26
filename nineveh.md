# HAck the Box - Nineveh


## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.43 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.43
Host is up (0.19s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https
```

```CSS
▶ nmap -sC -sV -p 80,443 10.10.10.43 -oN deep.nmap

Nmap scan report for 10.10.10.43
Host is up (0.18s latency).

PORT    STATE SERVICE  VERSION
80/tcp  open  http     Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
443/tcp open  ssl/http Apache httpd 2.4.18 ((Ubuntu))
| ssl-cert: Subject: commonName=nineveh.htb/organizationName=HackTheBox Ltd/stateOrProvinceName=Athens/countryName=GR
| Not valid before: 2017-07-01T15:03:30
|_Not valid after:  2018-07-01T15:03:30
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
```
