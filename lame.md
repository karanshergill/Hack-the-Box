# Hack the Box - Lame

```CSS
Machine IP: 10.10.10.3 - Linux
Difficulty: Easy
Category: OSCP Preparation
Vulmerabilities:
  - CVE-2011-2523: vsftpd 2.3.4 - Backdoor Command Execution
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

---

## Port 21 - FTP
  - Service and Version:`vsftpd 2.3.4`
  - Anonymous login is allowed.
![image](https://user-images.githubusercontent.com/83878909/236660813-dfffeaff-5498-4751-9611-33ed709a53c3.png)

```CSS
▶ ftp 10.10.10.3
```

  - No useful information was found.
![image](https://user-images.githubusercontent.com/83878909/236660787-9747600c-2dc6-4367-8179-e390ddcc588e.png)

### vsfptd 2.3.4
  - Check if the version is vulnerable using NMAP.
  - Search for a NMAP script to check `ftp` service.
```CSS
▶ ls /usr/share/nmap/scripts/ftp*
```
![image](https://user-images.githubusercontent.com/83878909/236664752-1a4b5dc8-8d51-49c3-b571-ab4953cf5983.png)

```CSS
▶ nmap -p 21 10.10.10.3 --script ftp-vsftpd-backdoor.nse
```
![image](https://user-images.githubusercontent.com/83878909/236664883-3430962a-ccbe-4d05-8348-9ff8ae89c375.png)
  - The above output shows that the target is not vulnerable.

---

## Port 139 & 445 - SMB (Samba)
  - Service and Version: `Samba 3.0.20 Debian`
![image](https://user-images.githubusercontent.com/83878909/236665134-25d9feb4-5cd8-4dc4-aadb-5871a4b3b898.png)

  - List Shares Anonymous
```CSS
▶ smbclient -L \\lame.hackthebox.gr -I 10.10.10.3 -N 
```
![image](https://user-images.githubusercontent.com/83878909/236665450-f2a18dcd-6de5-4c71-8a07-40edb57313d8.png)

  - View Share Permisssions
```CSS
▶ smbmap -H 10.10.10.3
```
![image](https://user-images.githubusercontent.com/83878909/236667248-57476b99-3660-4588-988d-06b7be5d5c86.png)

---

## Port 3632 distccd v1
  - Check if the version is vulnerable using NMAP.
  - Search for a NMAP script to check `distccd` service.

```CSS
▶ ls /usr/share/nmap/scripts/dist*
```
![image](https://user-images.githubusercontent.com/83878909/236667913-e01b1c12-28a9-4a99-a8ad-8abaaf12d65f.png)

```CSS
▶ nmap -Pn -p 3632 10.10.10.3 --script distcc-cve2004-2687.nse
```
![image](https://user-images.githubusercontent.com/83878909/236667868-56a68f3d-9a51-412f-b315-9b62fb71ec49.png)
