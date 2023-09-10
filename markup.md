# Hack the Box - Markup
```
rustscan -a 10.129.95.192 -r 0-65535
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cec0ae28-e40a-4d3a-85da-23fabd94e6c2)

```
nmap -Pn -sC -sV -p 22,80,43 10.129.95.192 --min-rate 1000 -oN service.scan
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/24951359-dfa5-4c34-9c72-eea065ca6486)

HTTP:80
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4a2e0956-7829-4e84-8572-a3a0a7c6d224)

Content Discovery
```
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-small.txt:FUZZ -u http://10.129.95.192/FUZZ -mc 200 -t 10 -c
```

Default Credentials
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a41685ee-dd5f-4651-bc75-aac3d405e430)
```
admin:admin
administrator:administrator
admin:administrator
admin:password
administrator:password
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9c5a32c2-cbf5-41a7-a75e-d68eb90c1f2c)

Login successful using default credentials `admin:password`.
