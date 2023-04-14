# Hack the Box - Blue
```CSS
Machine IP: 10.10.10.40
```

- NMAP Scans
  - [TCP all ports](# NMAP-TCP-All-Ports)
  - [TCP service version and default scripts of open ports]()
  - [TCP port #445 safe scripts]()

## NMAP (TCP - All Ports)
```CSS
▶ nmap -Pn -sS -p- 10.10.10.40 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.40                                        
Host is up (0.19s latency).                                             
Not shown: 65526 closed tcp ports (reset)                                                                                                        
PORT      STATE SERVICE                                                 
135/tcp   open  msrpc                                                   
139/tcp   open  netbios-ssn                                             
445/tcp   open  microsoft-ds                                            
49152/tcp open  unknown                                                 
49153/tcp open  unknown                                                 
49154/tcp open  unknown                                                                                                                          
49155/tcp open  unknown
49156/tcp open  unknown
49157/tcp open  unknown
                                    
Nmap done: 1 IP address (1 host up) scanned in 70.46 seconds
```

## NMAP (TCP - Open Ports: Service Version and Default Scripts)
```CSS
▶ nmap -sC -sV -p 135,139,445,49152-49157 10.10.10.40 -oN deep.nmap

Nmap scan report for 10.10.10.40                                                                                                           [0/21]
Host is up (0.18s latency).                                             
                                                                                                                                                 
PORT      STATE SERVICE      VERSION                           
135/tcp   open  msrpc        Microsoft Windows RPC                      
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn              
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)                                      
49152/tcp open  msrpc        Microsoft Windows RPC                      
49153/tcp open  msrpc        Microsoft Windows RPC                      
49154/tcp open  msrpc        Microsoft Windows RPC                      
49155/tcp open  msrpc        Microsoft Windows RPC                      
49156/tcp open  msrpc        Microsoft Windows RPC                      
49157/tcp open  msrpc        Microsoft Windows RPC                      
Service Info: Host: HARIS-PC; OS: Windows; CPE: cpe:/o:microsoft:windows                                                                         
                                    
Host script results:   
| smb2-security-mode:  
|   210:                            
|_    Message signing enabled but not required              
| smb2-time:                                                                                                                                     
|   date: 2023-04-13T17:38:57                                           
|_  start_date: 2023-04-13T17:27:27
| smb-security-mode:       
|   account_used: guest             
|   authentication_level: user                                          
|   challenge_response: supported                                       
|_  message_signing: disabled (dangerous, but default)    
| smb-os-discovery:                                                                                                                              
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)                                                                  
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: haris-PC                                             
|   NetBIOS computer name: HARIS-PC\x00           
|   Workgroup: WORKGROUP\x00                                            
|_  System time: 2023-04-13T18:38:56+01:00        
|_clock-skew: mean: -20m14s, deviation: 34m36s, median: -15s                                                                                     

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .                                                   
Nmap done: 1 IP address (1 host up) scanned in 75.47 seconds
```

## NMAP (TCP #445 Safe Scripts)
```CSS
▶ nmap -Pn -n -p 445 --script safe -oN safe.nmap

<---SNIP--->

| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
| port-states: 
|   tcp: 
|_    open: 445
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     202
|_    210
|_path-mtu: 1006 <= PMTU < 1492
|_clock-skew: mean: -20m12s, deviation: 34m33s, median: -15s

Post-scan script results:
| reverse-index: 
|_  445/tcp: 10.10.10.40
# Nmap done at Thu Apr 13 23:22:33 2023 -- 1 IP address (1 host up) scanned in 106.08 seconds
```
