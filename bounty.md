# Hack the Box - Bounty

```CSS
rustscan -a 10.10.10.93 -r 0-65535 --ulimit 5000
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7330b783-2899-4178-85f9-f2f4205e5751)

```CSS
nmap -sC -sV 10.10.10.93 -p 80
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/059852ea-43b3-440b-b772-658fba2b0935)

HTTP:80
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0e11f480-8ace-4ef6-8508-72abc975ffac)

HTTP:80 (Source-Code)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b9dfdf95-1160-4519-9a1c-41ac0f452e27)

Directory Fuzzing
```CSS
feroxbuster -u http://10.10.10.93 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -n
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e055ef8b-a99f-477d-8796-95a910bb9a76)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2141f6c4-5b42-48ae-9379-0f2fb9bdb62e)

File Fuzzing
```CSS
feroxbuster -u http://10.10.10.93 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -x aspx -s 200 -n
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/17b59a3d-7084-471b-b337-854971c477d4)

Secure File Transfer: File Upload
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e3bc0a21-f5cb-4a33-98e9-69b7adf437f9)
