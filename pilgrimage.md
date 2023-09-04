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