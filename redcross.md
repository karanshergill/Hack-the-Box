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

## Application Mapping
![image](https://user-images.githubusercontent.com/83878909/229340988-396c149d-59a9-44df-8bb8-846e1a2e6f3b.png)

### Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb --wordlist /usr/share/wordlists/directories.txt --threads 25 --no-tls-validation --output intra-dir.out
```
![image](https://user-images.githubusercontent.com/83878909/229342980-9b448de6-1f32-417a-915b-d419ef3afc08.png)

### Recursive Directory Brute-Force
```CSS
▶ gobuster dir --url https://intra.redcross.htb/pages --wordlist Common-PHP-Filenames.txt --no-tls-validation --threads 25 --output intra-dir-pages.out 
```
![image](https://user-images.githubusercontent.com/83878909/229349757-4437bdf3-24b6-4b47-aa87-b392ff82f9da.png)
