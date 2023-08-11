# HTB - Beep

## NMAP
```CSS
▶ nmap -Pn -sS -T4 --min-rate 5000 -p- 10.10.10.7

Nmap scan report for 10.10.10.7
Host is up (0.29s latency).
Not shown: 65519 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh 
25/tcp    open  smtp
80/tcp    open  http   
110/tcp   open  pop3
111/tcp   open  rpcbind
143/tcp   open  imap   
443/tcp   open  https
878/tcp   open  unknown
993/tcp   open  imaps
995/tcp   open  pop3s
3306/tcp  open  mysql    
4190/tcp  open  sieve  
4445/tcp  open  upnotifyp
4559/tcp  open  hylafax         
5038/tcp  open  unknown
10000/tcp open  snet-sensor-mgmt

Nmap done: 1 IP address (1 host up) scanned in 19.06 seconds
```

```CSS
▶ nmap -Pn -sC -sV -T4 --min-rate 5000 -p 22,25,80,110,111,143,443,878,993,995,3306,4190,4445,4459,5038,10000 10.10.10.7


```
