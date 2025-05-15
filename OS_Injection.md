# OS Command Injection

  OS Injection also known as shell injection, allows attackers to execute OS commands on the server that is running on an application.

  Command injection is possible when application passes unsafe input supplied by the user to a system shell.

  ## Example of Command Injection
  The vulnerable shopping application, has a stocker checker, lets user view wheter an item is in stock or not.

  Below is the screenshot of the request and response of this functionality.

  ![image](https://github.com/user-attachments/assets/89f9695c-e02d-4a73-8533-c372a71ac946)

  Above request stock check for product id = 1 and store id =1.

  ![image](https://github.com/user-attachments/assets/f121e539-cb51-461c-855a-6ed98d08f4b9)

  Response from the server to the application shows there are 62 items left.


  The request can be modified by the atatcker to retrieve sensitive data from the server. Such Injection Whoami command to the request retrieves the name of the current user.

  Command Injection at request:

  ![image](https://github.com/user-attachments/assets/9349bba1-a0f2-4828-a1e8-34450338e1d6)

  Response from server:

  ![image](https://github.com/user-attachments/assets/dca550c3-6285-4c37-a08b-0ba3de92b253)

---
  ## Usefull Commands for Injection

  | Purpose of Command | Linux | Windows |
  | -------------------- | --------------- | --------------- |
  | Name of current user | whoami | whoami |
  | Operating system | uname -a | ver |
  | Network configuration | ifconfig | ipconfig/all |
  | Network connections | netstat -an | netstat -an |
  |Running processes | ps -ef | tasklist |

  ## Ways of injecting OS commands

  Use shell characters to inject OS commands. 
  - &
  - &&
  - |
  - ||

---
## How to Prevent OS Injection

- Never call out OS commands from application layer.
- If application has to call out OS commands, use strong input validation.
    - Validating against a whitelist of permitted values.
    - Validating that the input is a number.
    - Validating that the input contains only alphanumeric characters, no other syntax or whitespace.
  

