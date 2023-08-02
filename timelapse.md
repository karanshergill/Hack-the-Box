# NMAP Scans
```CSS
nmap -Pn -sS -T4 --min-rate 1000 10.10.11.152 

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-02 17:41 IST
Nmap scan report for timelapse.htb (10.10.11.152)
Host is up (0.25s latency).
Not shown: 989 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl

Nmap done: 1 IP address (1 host up) scanned in 3.45 seconds
```
