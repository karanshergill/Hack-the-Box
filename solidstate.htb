# Hack the Box - SolidState

```CSS
Machine IP: 10.10.10.51
```

# Reconnaissance
  - Scan for open TCP ports on target machine.
  - Perform service and version detection of open ports.

## Port Scan
```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.51 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.51
Host is up (0.13s latency).
Not shown: 65509 closed tcp ports (reset)
PORT      STATE    SERVICE    
22/tcp    open     ssh    
25/tcp    open     smtp   
110/tcp   open     pop3   
119/tcp   open     nntp   
4555/tcp  open     rsip   
8147/tcp  filtered unknown
10189/tcp filtered unknown
21305/tcp filtered unknown
21847/tcp filtered netspeak-cs
28289/tcp filtered unknown
29998/tcp filtered unknown
32017/tcp filtered unknown    
32080/tcp filtered unknown
33752/tcp filtered unknown
33994/tcp filtered unknown
35039/tcp filtered unknown
36447/tcp filtered unknown
36542/tcp filtered unknown                                                                                                                                                 
37848/tcp filtered unknown
40496/tcp filtered unknown                                                           
45054/tcp filtered invision-ag                                                       
46627/tcp filtered unknown                                                           
55899/tcp filtered unknown                                                           
57996/tcp filtered unknown                                                           
60782/tcp filtered unknown                                                           
64762/tcp filtered unknown                                                           
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/7%OT=22%CT=1%CU=40233%PV=Y%DS=2%DC=I%G=Y%TM=6457A1D7
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=10B%TI=Z%CI=I%II=I%TS=8)OPS(
OS:O1=M53CST11NW7%O2=M53CST11NW7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST11
OS:NW7%O6=M53CST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN(
OS:R=Y%DF=Y%T=40%W=7210%O=M53CNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS                                                                                                
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=      
OS:R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T
OS:=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=
OS:S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 108.15 seconds
```

## Service and Version Detection
```CSS
▶ nmap -sC -sV -p 22,25,110,119,4555,8147,10189,21305,21847,28289,29998,32017,32080,33752,33994,35039,36447,36542,37848,40496,45054,46627,55899,57996,60782,64762 10.10.10.51 -oN services.nmap
```

---

