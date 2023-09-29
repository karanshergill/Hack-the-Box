# Hack the Box - Escape

```shell
root@kali# rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.202 -- -Pn
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.202:53
Open 10.10.11.202:88
Open 10.10.11.202:135
Open 10.10.11.202:139
Open 10.10.11.202:389
Open 10.10.11.202:445
Open 10.10.11.202:464
Open 10.10.11.202:593
Open 10.10.11.202:636
Open 10.10.11.202:5985
Open 10.10.11.202:9389
Open 10.10.11.202:49667
Open 10.10.11.202:49687
Open 10.10.11.202:49688
Open 10.10.11.202:49709
Open 10.10.11.202:49717
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.11.202
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-29 12:29 IST
Initiating Parallel DNS resolution of 1 host. at 12:29
Completed Parallel DNS resolution of 1 host. at 12:29, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:29
Scanning 10.10.11.202 [16 ports]
Discovered open port 53/tcp on 10.10.11.202
Discovered open port 135/tcp on 10.10.11.202
Discovered open port 139/tcp on 10.10.11.202
Discovered open port 445/tcp on 10.10.11.202
Discovered open port 593/tcp on 10.10.11.202
Discovered open port 49717/tcp on 10.10.11.202
Discovered open port 389/tcp on 10.10.11.202
Discovered open port 88/tcp on 10.10.11.202
Discovered open port 464/tcp on 10.10.11.202
Discovered open port 49709/tcp on 10.10.11.202
Discovered open port 49687/tcp on 10.10.11.202
Discovered open port 49688/tcp on 10.10.11.202
Discovered open port 49667/tcp on 10.10.11.202
Discovered open port 636/tcp on 10.10.11.202
Discovered open port 9389/tcp on 10.10.11.202
Discovered open port 5985/tcp on 10.10.11.202
Completed Connect Scan at 12:29, 0.29s elapsed (16 total ports)
Nmap scan report for 10.10.11.202
Host is up, received user-set (0.14s latency).
Scanned at 2023-09-29 12:29:19 IST for 0s

PORT      STATE SERVICE        REASON
53/tcp    open  domain         syn-ack
88/tcp    open  kerberos-sec   syn-ack
135/tcp   open  msrpc          syn-ack
139/tcp   open  netbios-ssn    syn-ack
389/tcp   open  ldap           syn-ack
445/tcp   open  microsoft-ds   syn-ack
464/tcp   open  kpasswd5       syn-ack
593/tcp   open  http-rpc-epmap syn-ack
636/tcp   open  ldapssl        syn-ack
5985/tcp  open  wsman          syn-ack
9389/tcp  open  adws           syn-ack
49667/tcp open  unknown        syn-ack
49687/tcp open  unknown        syn-ack
49688/tcp open  unknown        syn-ack
49709/tcp open  unknown        syn-ack
49717/tcp open  unknown        syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.32 seconds
```

Open Ports: 
