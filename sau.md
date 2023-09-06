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
