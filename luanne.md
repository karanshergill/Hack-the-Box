# Hack the Box - Luanne

```CSS
Machine IP: 10.10.10.218
```

```CSS
▶ sudo nmap -Pn -sS -O -p- 10.10.10.218 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.218
Host is up (0.18s latency).
Not shown: 35008 closed tcp ports (reset), 30524 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
9001/tcp open  tor-orport
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/20%OT=22%CT=2%CU=41916%PV=Y%DS=2%DC=I%G=Y%TM=6468388
OS:D%P=x86_64-pc-linux-gnu)SEQ(SP=DA%GCD=1%ISR=DD%TI=Z%CI=Z%II=I)OPS(O1=M53
OS:CNW3ST11%O2=M53CNW3ST11%O3=M53CNW3NNT11%O4=M53CNW3ST11%O5=M53CNW3ST11%O6
OS:=M53CST11)WIN(W1=8000%W2=8000%W3=8000%W4=8000%W5=8000%W6=8000)ECN(R=Y%DF
OS:=Y%T=40%W=8000%O=M53CNW3SLL%CC=N%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%
OS:Q=)T2(R=Y%DF=N%T=40%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=40%W=8000%
OS:S=O%A=S+%F=AS%O=M53CNW3ST11%RD=0%Q=)T4(R=Y%DF=N%T=40%W=0%S=A%A=Z%F=R%O=%
OS:RD=0%Q=)T5(R=Y%DF=N%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=N%T=40%W
OS:=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=N%T=40%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)U
OS:1(R=Y%DF=N%T=FF%IPL=38%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI
OS:=N%T=FF%CD=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 364.01 seconds
```

