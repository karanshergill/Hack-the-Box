# Hack the Box - Sense

```CSS
Machine IP: 10.10.10.60
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.60 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.60
Host is up (0.18s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 129.73 seconds
```

```CSS
▶ nmap -sC -sV -p 80,443 10.10.10.60 -oN deep.nmap

Nmap scan report for 10.10.10.60
Host is up (0.18s latency).

PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.10.10.60/
443/tcp open  ssl/http lighttpd 1.4.35
|_http-title: Login
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_http-server-header: lighttpd/1.4.35
|_ssl-date: TLS randomness does not represent time

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.14 seconds
```

