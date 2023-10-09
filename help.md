# Hack the Box - Help

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.121 -- -Pn
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
Please contribute more quotes to our GitHub https://github.com/rustscan/rustscan

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.121:22
Open 10.10.10.121:80
Open 10.10.10.121:3000
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-09 02:44 EDT
Initiating Parallel DNS resolution of 1 host. at 02:44
Completed Parallel DNS resolution of 1 host. at 02:44, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 02:44
Scanning 10.10.10.121 [3 ports]
Discovered open port 80/tcp on 10.10.10.121
Discovered open port 22/tcp on 10.10.10.121
Discovered open port 3000/tcp on 10.10.10.121
Completed Connect Scan at 02:44, 0.15s elapsed (3 total ports)
Nmap scan report for 10.10.10.121
Host is up, received user-set (0.15s latency).
Scanned at 2023-10-09 02:44:36 EDT for 0s

PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack
80/tcp   open  http    syn-ack
3000/tcp open  ppp     syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.23 seconds
```
