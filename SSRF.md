# Server Side Request forgery (SSRF)

  Web Security Vulnerability that allows an attcker to cause the server-side application to make request to an unintended location. In most cases, attacker might 
  make the server connect to internal service only, but also may force to connect to external systems, which could leak sensitive data.

  ## Impact of SSRF
  - Unauthorized access to data
  - Perform arbitary command execution
  - Connection to external 3rd party system (malicious onwards atatck)

  ### SSRF Attack against the server

  The attacker causes teh application to make an HTTP request back to the server that is hosting the application.

  Example of this Attack.

  Shopping Application, user can check for stock, the request is made to the server for that product and the response is displayed in the application.

  ```
  POST /product/stock HTTP/1.0
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 118

  stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
  ```

  Attacker can modify the above request and make the server redirect a specific URL.

  ```
  POST /product/stock HTTP/1.0
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 118

  stcokApi=http://localhost/admin
  ```
---

Why does this attack work?
  - Access control check is bypassed when request is made locally from the server.
  - Trust relationships, where requests originating from the local machine are handled differently than ordinary requests.
---

## Finding Attack surface for SSRF attacks

- Application's normal traffic invloves request parameters containing full URLs.
- Partial URLs in requests
- Referer header is often a useful attack surface for SSRF vulnerabilities.

## How to mitigate SSRF Attacks

  From Network Layer
  
    - Enforce deny by default firewall policy, block all but essential intranet traffic.
    - Segment remote resource access functionality in separate networks 
    
  From Application Layer
  
    - Sanitize and validate all user-supplied input data.
    - Enforce allow lists for URL schema.
    - Do not send raw response to client.
    - Disable HTTP redirection.
    
