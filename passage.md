# Hack the Box - Passage

```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.206 -- -Pn
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
Please contribute more quotes to our GitHub https://github.com/rustscan/rustscan

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.206:22
Open 10.10.10.206:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.10.206
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-27 16:04 IST
Initiating Parallel DNS resolution of 1 host. at 16:04
Completed Parallel DNS resolution of 1 host. at 16:04, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 16:04
Scanning 10.10.10.206 [2 ports]
Discovered open port 22/tcp on 10.10.10.206
Discovered open port 80/tcp on 10.10.10.206
Completed Connect Scan at 16:04, 0.15s elapsed (2 total ports)
Nmap scan report for 10.10.10.206
Host is up, received user-set (0.15s latency).
Scanned at 2023-09-27 16:04:27 IST for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.19 seconds
```
