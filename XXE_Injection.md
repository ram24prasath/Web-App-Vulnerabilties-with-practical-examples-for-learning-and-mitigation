# XML external entity (XXE) Injection 💉
  This atatck occurs when XML input containing a reference to an external entity is processed by a weakly configured XML parser.

  This attack may lead to disclosure of confidential data, denial of service, SSRF, port scanning from the perspective of the machine where parser is located.

  ### Types of XXE Attacks:
  - ***Exploiting XXE to retrieve files***: Where an external entity is defined containing the contents of the file and retured in applications response.
  - ***Exploiting XXE to perform SSRF***: Where an external entity is defined as URL to a back-end systems.
  - ***Exploiting blind XXE exfiltrate data out-of-band***: Sensitive data is transmitted from application server to a system that the atatcker controls.
  - ***Exploiting blind XEE to retrieve data via error message***: Attacker trigger a parsing error message containing sensitive data.


