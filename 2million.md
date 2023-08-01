## NMAP Scan
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f9b4668c-68c6-4114-b523-0f024af4b1c8)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/e50c6152-3712-4f06-9de5-f57966c064ae)

## Content Discovery
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b8b6ea67-e726-4542-8d83-7bf320db840d)

## 
```CSS
GoLinkFinder --domain http://2million.htb/ \
| grep -vE "\.css$|\.png$|\.jpg$|application/x-www-form-urlencoded|text/xml|text/plain|text/html|text/css|text/png|image/png" \
| sed '/^\s*$/d' \
| sort -u
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9b5d3d5e-ecd8-4255-af8c-53593846158a)

Invite API:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2b716221-48eb-4bb9-8c87-67ff7af3371f)

JS File (/js/inviteapi.min.js):
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ef41489b-d2a3-4252-b23c-3fcd4739c977)

Deobfuscated and Unpaked Code:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0fd3fd9d-79ec-4ca4-a89f-2f78b421f98c)

BurpSuite "POST" request:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3f352610-464e-4f7a-9514-2f62704ba7e2)

Curl "POST" request:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c48c6149-93c9-4cc5-9ea8-a4d59c181718)

Decode ROT 13:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8d080ae6-7b10-4989-8fbf-1d8c85b2a237)

BurpSuite "POST" request to generate invite code:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f18d354c-289d-4c75-94b2-d1710998a2dc)

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

Route List:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/2d6341f6-18cd-4304-833f-eab7b10a44c3)

Is Admin:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b5944855-e079-4028-b290-376f7d2b7cbd)

Escalate to Admin:
Send PUT request to /api/v1/admin/settings/update:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ae362cf1-f30c-48c2-96e0-44a2b5545e2e)

Verify Admin:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/9920a5f0-a730-45d7-bdc8-3be8c2f88ad5)

Command Injection:
VPN file generation end-point
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5e179418-e2d2-44e5-93e9-2a60780b77f0)



