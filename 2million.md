![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f9b4668c-68c6-4114-b523-0f024af4b1c8)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e50c6152-3712-4f06-9de5-f57966c064ae)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b8b6ea67-e726-4542-8d83-7bf320db840d)
```CSS
GoLinkFinder --domain http://2million.htb/ \
| grep -vE "\.css$|\.png$|\.jpg$|application/x-www-form-urlencoded|text/xml|text/plain|text/html|text/css|text/png|image/png" \
| sed '/^\s*$/d' \
| sort -u
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9b5d3d5e-ecd8-4255-af8c-53593846158a)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6ba312ef-250e-4656-8bee-c51d75b241ad)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/fd9dc172-9886-4b28-8962-7be3ded751a3)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c7668030-3c04-4f97-9741-217dfeac01c2)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/6c1dde86-0d63-4961-83c2-c57a4e24046b)

Deobfuscated and Unpaked Code:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/a3262db5-961b-4988-9b20-dadefc3dc2f6)

BurpSuite "POST" request:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3f352610-464e-4f7a-9514-2f62704ba7e2)

Curl "POST" request:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/62afc69f-00bb-4e16-a223-d9f5fc1e1ef3)


![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c05daab2-a9d8-4edc-a4f1-bd4283d70534)

POST request to generate invite code:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2521be49-4264-457e-913a-7a11f815e9c5)

Decode invite code:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/60e33920-c0bc-452c-8507-a963ddca5c51)

Invite code form:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3de52c84-8f83-459c-b6b8-94b7a8d1db88)
```
http://2million.htb/invite
```
Registration form:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/daff1891-7a13-4c2b-a212-83ed57d52a2f)
```
http://2million.htb/register
```
Login:
```
http://2million.htb/login
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/87cdd7d9-6597-4b08-9b96-03ae781794cc)

User Dashboard:
```CSS
http://2million.htb/home
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4435ad90-cddc-4709-8216-518ddce50685)
