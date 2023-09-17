# Hack the Box - Driver

```CSS
rustscan -a 10.10.11.106 -r 0-65535 --ulimit 5000
```
```
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
Open 10.10.11.106:80
Open 10.10.11.106:135
Open 10.10.11.106:445
Open 10.10.11.106:5985
[~] Starting Script(s)
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-17 12:05 IST
Initiating Ping Scan at 12:05
Scanning 10.10.11.106 [2 ports]
Completed Ping Scan at 12:05, 0.15s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 12:05
Completed Parallel DNS resolution of 1 host. at 12:05, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:05
Scanning 10.10.11.106 [4 ports]
Discovered open port 80/tcp on 10.10.11.106
Discovered open port 135/tcp on 10.10.11.106
Discovered open port 445/tcp on 10.10.11.106
Discovered open port 5985/tcp on 10.10.11.106
Completed Connect Scan at 12:05, 0.15s elapsed (4 total ports)
Nmap scan report for 10.10.11.106
Host is up, received syn-ack (0.15s latency).
Scanned at 2023-09-17 12:05:49 IST for 0s

PORT     STATE SERVICE      REASON
80/tcp   open  http         syn-ack
135/tcp  open  msrpc        syn-ack
445/tcp  open  microsoft-ds syn-ack
5985/tcp open  wsman        syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.39 seconds
```
