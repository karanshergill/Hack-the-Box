# Hack the Box - Nineveh


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

---

## HTTP
![image](https://user-images.githubusercontent.com/83878909/234479646-7b054e0f-a213-479e-9a80-3d63bdcbb1ef.png)

---

## HTTPS/SSL
![image](https://user-images.githubusercontent.com/83878909/234479727-ccec4c69-ee5a-4d14-b0ac-20744987d630.png)

---

## Content Discovery
  - Directory brute-force - `http://nineveh.htb`
```CSS
▶ gobuster dir -u nineveh.htb -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```
![image](https://user-images.githubusercontent.com/83878909/234485858-a451bd36-d418-447e-924a-bdecc2cd8c61.png)
![image](https://user-images.githubusercontent.com/83878909/234485999-3f3e259c-2a1d-420a-ac1f-4a41b74b2480.png)

  - Directory brute-force - `https://nineveh.htb`
```CSS
▶ gobuster dir -u https://nineveh.htb -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 50 --no-tls-validation
```
![image](https://user-images.githubusercontent.com/83878909/234484978-13d104de-2e36-46c6-8f17-fbb217cf826e.png)

