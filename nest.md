# Hack the Box - Nest

```CSS
rustscan -a 10.10.10.178 -r 0-65535 --ulimit 5000
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/f8da461f-072a-4053-9bd3-4d32ea29e5f3)

```CSS
crackmapexec smb 10.10.10.178
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/76ffbf1e-765e-4337-8453-9b6c1cb6f562)

```CSS
crackmapexec smb 10.10.10.178 -u 'anonymous' -p '' --shares
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/d1462bd8-e064-4449-9345-939825a37550)

```CSS
smbclient -N //10.10.10.178/Data
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/580c8eb6-cf7b-4454-ae81-08a0704618b1)

```CSS
smbclient -N //10.10.10.178/Users
```
![image](https://github.com/karanshergill/Hack-the-Box/assets/83878909/b9e2953b-49d1-4592-8b6e-2c48619a5f63)
