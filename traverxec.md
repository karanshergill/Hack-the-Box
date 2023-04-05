# Hack the Box - Traverxec

```CSS
Machine IP: 10.10.10.165 - Linux
Webserver: Nostromo 1.9.6

Vulnerabilities:
  - CVE-2019-16278 (Nostromo: Path Traversal and Command Execution)
```

## Server:
- Nostromo 1.9.6
![image](https://user-images.githubusercontent.com/83878909/229997880-3f1414ac-da7d-48ab-8025-146541085139.png)

## Port-80 (HTTP)
- Home Page
![image](https://user-images.githubusercontent.com/83878909/229997572-6322b2e8-9af1-4c06-aad8-c706c98a0b27.png)

---

# Exploit
![image](https://user-images.githubusercontent.com/83878909/230005962-a408db0c-096d-4409-87fd-54a513a69896.png)

### Path Traversal and Command Execution
![image](https://user-images.githubusercontent.com/83878909/230006489-a47d88d4-c2f0-40ea-baaa-5ee8930fe14c.png)

![image](https://user-images.githubusercontent.com/83878909/230008238-17e20208-9f10-48a8-b2c6-aa782ddc1645.png)

### Shell Upgrade
![image](https://user-images.githubusercontent.com/83878909/230012750-9484c874-7daf-4e16-a42e-24f309abed30.png)

## Lateral Movement
### Target Enumeration
  - LinPEAS 
![image](https://user-images.githubusercontent.com/83878909/230016737-2c8ebc40-6e3e-44ce-9e0a-155df8d36c9b.png)
  - LinEnum
![image](https://user-images.githubusercontent.com/83878909/230021523-9877eab9-f69a-42fe-bcca-0444abd9c93a.png)
  - Credentials: `david:$1$e7NfNpNi$A6nCwOTqrNR2oDuIKirRZ/`

### Crack the Password Hash
```CSS
▶ hashcat -m 500 -a 3 david.htpasswd /usr/share/wordlists/rockyou.txt
```
- Password: 
- Did not prove to be uselful.

### Further Enumeration
![image](https://user-images.githubusercontent.com/83878909/230030105-bc3eb668-ce7f-4844-9188-1ef435299bdb.png)
![image](https://user-images.githubusercontent.com/83878909/230030844-f2ad8410-043f-4f35-9d96-3dc1c9e3fe5d.png)
![image](https://user-images.githubusercontent.com/83878909/230031724-3996cd72-8103-443c-af1a-a186d92a5bc0.png)

  - ZIP Contents
![image](https://user-images.githubusercontent.com/83878909/230033032-f4cd7613-d208-4c2e-b841-6dcf2c83a683.png)
  - Crack `id_rsa` to get SSH password.
![image](https://user-images.githubusercontent.com/83878909/230034179-973fb7a6-763c-413c-a4d6-80bc12f3af52.png)

### SSH
![image](https://user-images.githubusercontent.com/83878909/230034797-e5ee66ee-909f-4ec0-b799-352b455d438d.png)




