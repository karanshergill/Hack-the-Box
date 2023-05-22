# Hack the Box - Tabby

```CSS
Machine IP: 10.10.10.194 - Linux

```

---

```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.194 -T4 --min-rate 1000 -oN ports.nmap
Starting Nmap 7.93 ( https://nmap.org ) at 2023-05-22 11:08 IST
Nmap scan report for 10.10.10.194
Host is up (0.19s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8080/tcp open  http-proxy
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/22%OT=22%CT=1%CU=42207%PV=Y%DS=2%DC=I%G=Y%TM=646B001
OS:B%P=x86_64-pc-linux-gnu)SEQ(SP=FD%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)OPS(
OS:O1=M53CST11NW7%O2=M53CST11NW7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST11
OS:NW7%O6=M53CST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(
OS:R=Y%DF=Y%T=40%W=FAF0%O=M53CNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=
OS:R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T
OS:=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=
OS:S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 79.91 seconds
```

```CSS
▶ nmap -sC -sV -p 22,80,8080 10.10.10.194 -oN services.nmap
Starting Nmap 7.93 ( https://nmap.org ) at 2023-05-22 11:10 IST
Nmap scan report for 10.10.10.194
Host is up (0.17s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 453c341435562395d6834e26dec65bd9 (RSA)
|   256 89793a9c88b05cce4b79b102234b44a6 (ECDSA)
|_  256 1ee7b955dd258f7256e88e65d519b08d (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Mega Hosting
|_http-server-header: Apache/2.4.41 (Ubuntu)
8080/tcp open  http    Apache Tomcat
|_http-title: Apache Tomcat
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.13 seconds
```

---

# Port 80
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/bb960e94-7b85-470f-8501-04813c7744df)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a1ad3174-c498-4e0b-afc7-11faaf051616)
 
- Add the domain name `megahosting.htb` to the `/etc/hosts` file.
```CSS
▶ sudo -- sh -c "echo '10.10.10.194 megahosting.htb' >> /etc/hosts"
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/028519af-034e-4a45-993d-937fa894b7e1)

---

## Local File Inclusion (LFI)
We notice that we are being redirected to http://megahosting.htb/news.php?file=statement. It's worth noting that `statement` seems to be a filename passed as input to the parameter `file` of the page news.php . Let's check if this is vulnerable to Local File Inclusion (LFI), by trying to load the `/etc/passwd` file.

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/afb98396-df84-4b56-b9ef-ce367446f0f7)

---

# Port 8080
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/bb40c443-61df-487a-afdb-2559da6a6ee6)

---

### Content Discovery
Brute-force the URL path to look for some common hidden directories and files.
```CSS
▶ gobuster dir --url http://megahosting.htb:8080 --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/230e9c6b-b14c-4504-81aa-5dce91f80bd1)
Scanning reveals the well-known Tomcat `/manager` page. This is a default page that allows users to manage web applications.

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/2db1b182-901d-42aa-8e29-4770a7036509)
Tomcat's manager page requires authentication. Attempting to log in with common credentials like admin / admin is not successful.

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/b8d36d51-f02c-4ba2-af1f-730dd251cf30)
However, on clicking cancel we get a 401 Unauthorized message. This page reveals that the credentials are in the file `conf/tomcat-users.xml`. 

Navingating to the location of the `tomcat-users.xml` using the LFI as mentioned, returns a blank page.

Checking if the file `tomcat-users.xml` is located in a different path inside Tomcat's default installation directory.
- Tomcat default installation directory: `/usr/share/tomcat9/`.
- Default location of `tomcat-users.xml`: `etc/tomcat-users.xml`.

The final path should be: `/usr/share/tomcat9/etc/tomcat-users.xml`.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c5629bff-e6c1-4aff-9036-8681fa3cdf40)

The file contains the credentials tomcat / $3cureP4s5w0rd123!.
As the roles xml attribute shows that this user is a member of admin-gui and manager-script . The manager-gui role that allows access to the /manager page is not assigned.

Brute-force the URL path `/manager/` to look for some common hidden directories and files.
```CSS
▶ gobuster dir --url http://megahosting.htb:8080/manager --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/992d8893-58ec-4b66-888b-8968af93f140)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4f0c0678-6876-453b-92d0-76be836774fa)
