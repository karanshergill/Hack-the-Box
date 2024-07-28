# Hack the Box | Headless

```shell
rustscan -b 1000 -u 5000 -a 10.10.11.8 -r 0-65535
```
```shell
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.8:22
Open 10.10.11.8:5000
[~] Starting Script(s)
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2024-07-28 04:58 EDT
Initiating Ping Scan at 04:58
Scanning 10.10.11.8 [2 ports]
Completed Ping Scan at 04:58, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 04:58
Completed Parallel DNS resolution of 1 host. at 04:58, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 04:58
Scanning 10.10.11.8 [2 ports]
Discovered open port 22/tcp on 10.10.11.8
Discovered open port 5000/tcp on 10.10.11.8
Completed Connect Scan at 04:58, 0.11s elapsed (2 total ports)
Nmap scan report for 10.10.11.8
Host is up, received conn-refused (0.11s latency).
Scanned at 2024-07-28 04:58:24 EDT for 0s

PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack
5000/tcp open  upnp    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.27 seconds
```