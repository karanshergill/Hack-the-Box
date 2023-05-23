# Hack the Box - Resolute

# Enumeration
## NMAP
```CSS
▶ 
```

## RPC Client
  - Null Session Authentication
```CSS
▶ rpcclient -U "" -N 10.10.10.169
```

  - Enumerate Domain Users
```CSS
rpcclient $> enumdomusers
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/d4596127-4b1b-4957-ac1b-c0e30d6cd312)

  - Query Users Info
```CSS
rpcclient $> querydispinfo
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/ec7322f6-3ebb-4fb8-8691-c8c92af2dc0e)
The above command return brief information about all the users. An interesting comment for `RID 0x457` is also found.
```CSS
Credentials - marko:Welcome123!
```

  - Query Single User's Info
```CSS
rpcclient $> queryuser 0x1f4
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/56612aa0-fa48-41b2-ad95-e6cd47bf97a5)

