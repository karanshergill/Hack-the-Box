# Hack the Box: Authority

## Open Ports
```CSS
rustscan -b 1000 -a 10.10.11.222 -r 0-65535 -u 5000 -- -Pn
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.222:53
Open 10.10.11.222:80
Open 10.10.11.222:88
Open 10.10.11.222:135
Open 10.10.11.222:139
Open 10.10.11.222:389
Open 10.10.11.222:445
Open 10.10.11.222:464
Open 10.10.11.222:593
Open 10.10.11.222:636
Open 10.10.11.222:3268
Open 10.10.11.222:3269
Open 10.10.11.222:5985
Open 10.10.11.222:8443
Open 10.10.11.222:9389
Open 10.10.11.222:47001
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.11.222
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-24 15:26 IST
Initiating Parallel DNS resolution of 1 host. at 15:26
Completed Parallel DNS resolution of 1 host. at 15:26, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 15:26
Scanning 10.10.11.222 [16 ports]
Discovered open port 139/tcp on 10.10.11.222
Discovered open port 80/tcp on 10.10.11.222
Discovered open port 53/tcp on 10.10.11.222
Discovered open port 135/tcp on 10.10.11.222
Discovered open port 445/tcp on 10.10.11.222
Discovered open port 5985/tcp on 10.10.11.222
Discovered open port 636/tcp on 10.10.11.222
Discovered open port 3268/tcp on 10.10.11.222
Discovered open port 593/tcp on 10.10.11.222
Discovered open port 8443/tcp on 10.10.11.222
Discovered open port 3269/tcp on 10.10.11.222
Discovered open port 47001/tcp on 10.10.11.222
Discovered open port 88/tcp on 10.10.11.222
Discovered open port 389/tcp on 10.10.11.222
Discovered open port 464/tcp on 10.10.11.222
Discovered open port 9389/tcp on 10.10.11.222
Completed Connect Scan at 15:26, 0.31s elapsed (16 total ports)
Nmap scan report for 10.10.11.222
Host is up, received user-set (0.15s latency).
Scanned at 2023-09-24 15:26:04 IST for 0s

PORT      STATE SERVICE          REASON
53/tcp    open  domain           syn-ack
80/tcp    open  http             syn-ack
88/tcp    open  kerberos-sec     syn-ack
135/tcp   open  msrpc            syn-ack
139/tcp   open  netbios-ssn      syn-ack
389/tcp   open  ldap             syn-ack
445/tcp   open  microsoft-ds     syn-ack
464/tcp   open  kpasswd5         syn-ack
593/tcp   open  http-rpc-epmap   syn-ack
636/tcp   open  ldapssl          syn-ack
3268/tcp  open  globalcatLDAP    syn-ack
3269/tcp  open  globalcatLDAPssl syn-ack
5985/tcp  open  wsman            syn-ack
8443/tcp  open  https-alt        syn-ack
9389/tcp  open  adws             syn-ack
47001/tcp open  winrm            syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.34 seconds
```

## Exposed Services


### Port-80 HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/59af5066-2212-4520-a735-8d59161dfa52)

