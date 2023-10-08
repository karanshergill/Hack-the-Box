# Hack the Box - Holiday

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.25 -- -Pn
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.25:22
Open 10.10.10.25:8000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-08 12:45 EDT
Initiating Parallel DNS resolution of 1 host. at 12:45
Completed Parallel DNS resolution of 1 host. at 12:45, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:45
Scanning 10.10.10.25 [2 ports]
Discovered open port 8000/tcp on 10.10.10.25
Discovered open port 22/tcp on 10.10.10.25
Completed Connect Scan at 12:45, 0.14s elapsed (2 total ports)
Nmap scan report for 10.10.10.25
Host is up, received user-set (0.14s latency).
Scanned at 2023-10-08 12:45:50 EDT for 0s

PORT     STATE SERVICE  REASON
22/tcp   open  ssh      syn-ack
8000/tcp open  http-alt syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.21 seconds
```
