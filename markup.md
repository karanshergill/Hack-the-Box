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
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5ffaf41f-1fea-4c58-ac6a-62a1850a1f78)
Did not return any results.

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

![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/7742947e-777a-482f-ac54-9ca53cfa9b99)
Username: Daniel

XXE
The "order" page is interactive.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/5cec6e4c-bfec-4956-8415-b983e3c8d030)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/36dd1aa7-2fa6-49af-a84d-b3fcb3bf04f2)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/c5bd7af6-1bc7-4462-81dd-f868606fc482)
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/0d4ea184-3f8e-4daa-9c2a-eac458939105)

The website uses XML to send the order values to the server, could be vulnerable to XEE.
XEE: or XML External Entity attack is a type of attack against an application that parses XML input and allows XML entities. XML entities can be used to tell the XML parser to fetch specific content on the server.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b8428ea7-1b18-4d97-8764-a7bfccd1c0a7)
Vulnerable to XXE

Since a LFI exists, find SSH keys for the user Daniel.
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/8dc3e18c-7adf-4d4a-bcd3-c3f228046f07)

Save the Key to a file `id_rsa` and give permissions `chmod 600 id_rsa`.
Login with SSH
```
ssh daniel@10.129.95.192 -i id_rsa
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/dc03e956-1a0c-4815-9106-701802ef8ffb)

Privilege Escalation
Upload WinPEAS
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/3cef7999-c36e-49b1-a45c-1c10d9e77f95)

Easy Way:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/cc01220f-3f5f-494c-a006-f9a89735865d)

Hard Way:
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/348d23d7-3ad1-4846-bf01-003e2eb0b425)

