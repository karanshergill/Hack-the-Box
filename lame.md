# Hack the Box - Lame

```CSS
Machine IP: 10.10.10.3 - Linux
Difficulty: Easy
Category: OSCP Preparation
```

# Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

## Port Scan
```CSS
▶ nmap -Pn -sS -p- 10.10.10.3 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.3
Host is up (0.18s latency).
Not shown: 65530 filtered tcp ports (no-response)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3632/tcp open  distccd

Nmap done: 1 IP address (1 host up) scanned in 131.61 seconds
```

## Service and Version Detection
```CSS
▶ nmap -sC -sV -p 21,22,139,445,3632 10.10.10.3 -oN services.nmap

Nmap scan report for 10.10.10.3                                                      
Host is up (0.17s latency).                                                          
                                                                                     
PORT     STATE SERVICE     VERSION                                                   
21/tcp   open  ftp         vsftpd 2.3.4                                              
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)        
| ftp-syst: 
|   STAT:           
| FTP server status:                                                                 
|      Connected to 10.10.14.24
|      Logged in as ftp           
|      TYPE: ASCII     
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status          
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey:                   
|   1024 600fcfe1c05f6a74d69024fac4d56ccd (DSA)       
|_  2048 5656240f211ddea72bae61b1243de8f3 (RSA)                
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
3632/tcp open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
                                          
Host script results:
|_smb2-time: Protocol negotiation failed (SMB2)                                      
| smb-os-discovery:            
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: lame
|   NetBIOS computer name:       
|   Domain name: hackthebox.gr          
|   FQDN: lame.hackthebox.gr           
|_  System time: 2023-05-07T02:00:56-04:00
| smb-security-mode:                      
|   account_used: <blank>
|   authentication_level: user                                                       
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 1h59m43s, deviation: 2h49m43s, median: -17s
                                                                                     
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.82 seconds
```

## FTP
  - Anonymous login is allowed.
![image](https://user-images.githubusercontent.com/83878909/236660712-4559c6ec-0b42-49ce-878b-d9adbc56e116.png)
