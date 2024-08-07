# iClean

## Port Scan
```shell
rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.12
```
```rust
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
TCP handshake? More like a friendly high-five!

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.12:22
Open 10.10.11.12:80
[~] Starting Script(s)
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2024-08-07 10:41 IST
Initiating Ping Scan at 10:41
Scanning 10.10.11.12 [2 ports]
Completed Ping Scan at 10:41, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:41
Completed Parallel DNS resolution of 1 host. at 10:41, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:41
Scanning 10.10.11.12 [2 ports]
Discovered open port 22/tcp on 10.10.11.12
Discovered open port 80/tcp on 10.10.11.12
Completed Connect Scan at 10:41, 0.09s elapsed (2 total ports)
Nmap scan report for 10.10.11.12
Host is up, received conn-refused (0.089s latency).
Scanned at 2024-08-07 10:41:57 IST for 0s
PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.22 seconds
```
