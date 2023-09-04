# Hack the Box - Pilgrimage

### Port Scan
```JS
rustscan -a 10.10.11.219 -r 0-65535 --ulimit 5000
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e689b57a-a922-4249-bd1f-e9fa6a10c6b1)

### Service Scan
```JS
nmap -sV -sC -A --min-rate 1000 10.10.11.219 -p 22,80
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8e7088bb-eda7-48c9-a997-9aff249734e7)

### HTTP
#### /index.php
```
http://pilgrimage.htb/index.php
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/926d244a-ec49-4f00-b52e-2470dcf12de7)

#### /login.php
```
http://pilgrimage.htb/login.php
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/91c3655e-75c4-4434-a7c0-6cb6ffb4f416)

#### /register.php
```
http://pilgrimage.htb/register.php
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ae7ea9df-3379-4ae2-9bb1-21aab0840fb0)

#### /.git
```
http://pilgrimage,htb/.git/
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cf236a5d-c1d5-4e61-b79b-51f8ee5df32f)

### Dump /.git
```JS
git-dumper http://pilgrimage.htb/.git/ git
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8e034218-7ed2-4956-b0e3-821f84f9a665)
