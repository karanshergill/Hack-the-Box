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
rustscan -u 5000 -a 10.10.11.202 -p 53,88,135,139,389,445,464,593,636,5985,9389,49248,49667,49687,49688,49709,49717 -- -Pn -sC -sV
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
root@kali# echo "10.10.11.202    sequel.htb dc.sequel.htb" >> /etc/hosts
```
