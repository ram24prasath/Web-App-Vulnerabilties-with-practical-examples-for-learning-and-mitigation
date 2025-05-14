# XML external entity (XXE) Injection 💉
  This attack occurs when XML input containing a reference to an external entity is processed by a weakly configured XML parser.

  This attack may lead to disclosure of confidential data, denial of service, SSRF, port scanning from the perspective of the machine where parser is located.

  ### Types of XXE Attacks:
  - ***Exploiting XXE to retrieve files***: Where an external entity is defined containing the contents of the file and retured in applications response.
  - ***Exploiting XXE to perform SSRF***: Where an external entity is defined as URL to a back-end systems.
  - ***Exploiting blind XXE exfiltrate data out-of-band***: Sensitive data is transmitted from application server to a system that the atatcker controls.
  - ***Exploiting blind XEE to retrieve data via error message***: Attacker trigger a parsing error message containing sensitive data.

---

  ### Exploiting XXE using external entity to retrieve files.

  Following example is referred from port swingger web security academy, for more details check the reference section below.

  A shopping application (intentionally vulnerable web app) checks for stocks level for a product by submitting a following XML to the server.

  ```
    <?xml version="1.0" encoding="UTF-8"?>
    <stockCheck><productId>381</productId></stockCheck>
  ```

  To exploit XXE vulnerability and the task is to retrieve the contents of file /etc/passwd.

  ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
    <stockCheck><productId>&xxe;</productId></stockCheck>
  ```

  Once the crafted payload is sent to the server, the content of the file can be retrieved from the application's response.

  ![image](https://github.com/user-attachments/assets/ac82c5d3-06c8-41c5-a877-2a17d2bd9b7c)
