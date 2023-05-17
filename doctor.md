# Hack the Box - Doctor

```CSS 
Machine IP: 10.10.10.209
```

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.209 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.209
Host is up (0.21s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8089/tcp open  unknown
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 5.0 (97%), Linux 4.15 - 5.6 (92%), Linux 5.4 (90%), Crestron XPanel control system (90%), Linux 5.3 - 5.4 (90%), Linux 5.0 - 5.3 (89%), Linux 5.0 - 5.4 (88%), Linux 2.6.32 (88%), ASUS RT-N56U WAP (Linux 3.4) (87%), Linux 3.1 (87%)
No exact OS matches for host (test conditions non-ideal).

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 138.10 seconds
```

```CSS
▶ 
```
