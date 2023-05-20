# Hack the Box - BlackField


```CSS
Machine IP: 10.10.10.192
```

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.192 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.192
Host is up (0.18s latency).
Not shown: 65527 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
389/tcp  open  ldap
445/tcp  open  microsoft-ds
593/tcp  open  http-rpc-epmap
3268/tcp open  globalcatLDAP
5985/tcp open  wsman
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 135.41 seconds
```
