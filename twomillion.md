# Hack the Box - Two Million

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.221 -- -Pn
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
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.221:22
Open 10.10.11.221:80
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-10 04:32 EDT
Initiating Parallel DNS resolution of 1 host. at 04:32
Completed Parallel DNS resolution of 1 host. at 04:32, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 04:32
Scanning 10.10.11.221 [2 ports]
Discovered open port 22/tcp on 10.10.11.221
Discovered open port 80/tcp on 10.10.11.221
Completed Connect Scan at 04:32, 0.18s elapsed (2 total ports)
Nmap scan report for 10.10.11.221
Host is up, received user-set (0.19s latency).
Scanned at 2023-10-10 04:32:22 EDT for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.22 seconds
```
