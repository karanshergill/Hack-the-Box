# Hack the Box

## NMAP Scans
```CSS
> nmap -Pn -sS -T4 --min-rate 5000 -p- 10.10.11.209 -oN mailroom.surface                                           

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-22 01:12 IST
Nmap scan report for 10.10.11.209
Host is up (0.26s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 14.52 seconds
```
