# Hack the Box - Intelligence

```CSS
Nachine IP: 10.10.10.248
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.248 -T4 --min-rate 1000 -oN nmap.surface

Nmap scan report for 10.10.10.248
Host is up (0.18s latency).
Not shown: 65516 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
80/tcp    open  http
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49667/tcp open  unknown
49691/tcp open  unknown
49692/tcp open  unknown
49707/tcp open  unknown
49714/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 304.78 seconds
```

```CSS
▶ 
```
