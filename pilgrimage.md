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

## Interaction
### Create Account
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8aace601-5083-47e0-9097-4d362135c8cb)

### Login
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/59281814-60c3-4606-aa98-5b736e27baee)

### Dashboard
```
http://pilgrimage.htb/dashboard.php
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2baf238c-a0fd-4fa2-8492-96816f3450e4)

### Shrink Image
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/28416acf-9319-4a20-aca5-0f2477231c16)

### Shrunk Image
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/45222057-30a0-40cb-9236-277ac66f3cdb)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b7769831-449a-4948-ad62-33f08d6fbae5)

## Source Code
- The code uses "magick" to shrink the uploaded image.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e1e8ac77-b705-4a8a-a2f3-a1e887ede57d)

### Search Exploits
```
searchsploit magick
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/dfc0dea8-95b2-412e-9509-488bcf24d57e)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2a7440d9-e578-4433-a503-4c280c16ddd1)

### Exploit - Magick (Arbitrary File Read): CVE-2022-44268
The exploit allows to read arbitrary files on the server.
The suggested exploit has been scripted using rust. Using an explot scripted using python.
```
https://github.com/kljunowsky/CVE-2022-44268
```

