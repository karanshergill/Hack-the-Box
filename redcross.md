# Hack the Box - RedCross
```CSS
Machine IP: 10.10.10.113 - Debian
```
## Reconnaisance
**Disover all open TCP ports**
```CSS
▶ nmap -Pn -sS -p- 10.10.10.113 -T4 --min-rate 1000 -oN nmap.surface
```

**Identify and scan running services on open ports**
```CSS
▶ sudo nmap -sV -sC -p 22,80,443 10.10.10.113 -oN nmap.deep 
```

---

## Application Mapping
![image](https://user-images.githubusercontent.com/83878909/229340988-396c149d-59a9-44df-8bb8-846e1a2e6f3b.png)

---

### Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb --wordlist /usr/share/wordlists/directories.txt --no-tls-validation --threads 25 --output intra-dir.out
```
![image](https://user-images.githubusercontent.com/83878909/229342980-9b448de6-1f32-417a-915b-d419ef3afc08.png)

### Recursive Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb/pages --wordlist Common-PHP-Filenames.txt --no-tls-validation --threads 25 --output intra-dir-pages.out 
```
![image](https://user-images.githubusercontent.com/83878909/229349757-4437bdf3-24b6-4b47-aa87-b392ff82f9da.png)

### Recursive Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb/documentation --wordlist directory-list-2.3-small.txt --no-tls-validation  --threads 25 --output intra-dir-pages.out --extensions pdf,txt 
```
![image](https://user-images.githubusercontent.com/83878909/229352633-afb50fcf-6b44-47a5-ad7d-327324b03a67.png)

---

## Virtual Host Brute-Force
```CSS
▶ wfuzz -H 'Host: FUZZ.redcross.htb' -u 'https://10.10.10.113' -w subdomains-top1million-5000.txt --hw 28
```
![image](https://user-images.githubusercontent.com/83878909/229351137-705a4132-e00b-45b5-b551-2f9a15acb448.png)

---

## Testing for SQL Injection
  - URL: `https://intra.redcross.htb/?page=login`
  - Capture the request in BurpSuite and copy it to a text file using `Copy to file`.
  - Run `sqlmap` with the captured request. 
![image](https://user-images.githubusercontent.com/83878909/229352907-4b619112-09b4-4d94-bb9e-af767ebf9e9a.png)
![image](https://user-images.githubusercontent.com/83878909/229352924-ffbba2d9-f739-43a1-b7fa-98c14ad39f6e.png)

### SQLMap
```CSS
▶ sqlmap -r login-request.txt --force-ssl --dbms mysql --batch
```
**NOT VULNERABLE**

---

## Testing for Default Credentials on Login Page
- Logged in as Guest.
- Working credentials: `guest:guest`.
![image](https://user-images.githubusercontent.com/83878909/229353512-1722be64-2483-4f6e-aa8c-ee2d70a9786a.png)
