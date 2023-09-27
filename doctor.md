# Hack the Box - Doctor

```shell
root@kali# rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.10.209 -- -Pn
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
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.209:22
Open 10.10.10.209:80
Open 10.10.10.209:8089
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.10.209
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-27 13:24 IST
Initiating Parallel DNS resolution of 1 host. at 13:24
Completed Parallel DNS resolution of 1 host. at 13:24, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 13:24
Scanning 10.10.10.209 [3 ports]
Discovered open port 80/tcp on 10.10.10.209
Discovered open port 22/tcp on 10.10.10.209
Discovered open port 8089/tcp on 10.10.10.209
Completed Connect Scan at 13:24, 0.15s elapsed (3 total ports)
Nmap scan report for 10.10.10.209
Host is up, received user-set (0.15s latency).
Scanned at 2023-09-27 13:24:41 IST for 0s

PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack
80/tcp   open  http    syn-ack
8089/tcp open  unknown syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.19 seconds
```

## HTTP 80
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4fdf842b-3b62-46fd-8ce2-de8b1d5aec36)

## Virtual Host
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/975f588d-00eb-445d-86b5-6d5329c73a4a)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c4ff87b3-8fb5-4997-b54e-73d290e0cbf5)
