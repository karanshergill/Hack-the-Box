# NMAP
```CSS
▶ nmap -Pn -sS -p- -T4 --min-rate 1000 10.10.10.215

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-03 10:48 IST
Nmap scan report for 10.10.10.215
Host is up (0.25s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
33060/tcp open  mysqlx

Nmap done: 1 IP address (1 host up) scanned in 70.45 seconds
```
