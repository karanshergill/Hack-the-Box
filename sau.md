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
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7b31d1f4-54ea-4192-89a2-d8c133665324)
