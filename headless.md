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

![image](https://github.com/user-attachments/assets/3f8bfa63-74f2-45f5-bf57-0aa09aab8802)
![image](https://github.com/user-attachments/assets/7f735d8a-1c76-438f-869c-7a5ef2bcf244)
![image](https://github.com/user-attachments/assets/cf9b28f5-7fae-4ee1-9987-c46479da10be)
![image](https://github.com/user-attachments/assets/480f95e3-2ac1-4db1-a882-33250ba8247f)
```
fname=Ricky&lname=1337&email=ricky%40hackme.com&phone=9879879870&message=<script>alert('XSS')</script>
```
![image](https://github.com/user-attachments/assets/b43b8b99-2efb-4feb-a712-da2b2e09dd35)

```shell
feroxbuster -u http://10.10.11.8:5000 -w /usr/share/seclists/Discovery/Web-Content/RobotsTxtPaths-Trickest-Wordlists/top-10000-websites.txt --no-recursion --dont-extract-links --random-agent --filter-status 404 --redirects --filter-words 259
```
