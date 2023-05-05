# Hack the Box - Jeeves

```CSS
Machine IP: 10.10.10.63
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.63 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.63
Host is up (0.18s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT      STATE SERVICE
80/tcp    open  http
135/tcp   open  msrpc
445/tcp   open  microsoft-ds
50000/tcp open  ibm-db2

Nmap done: 1 IP address (1 host up) scanned in 126.42 seconds
```

