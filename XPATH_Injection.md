# **XPATH Injection**

  _XPath Injection attacks occurs when a website uses user-supplied input directly in XPATH query for XML Data._ 

## Description
  Attacker sends intentionally malformed information to the input fields in the web application, by doing this attacker can find out the structure of XML data, access information and they dont have access to, may even elevate their privilege if XML data is being used for authentication.
  
## Example Vulnerable XML Code

XML is eXtensible markup language like HTML. Designed to store and transport data. 

XPath can be used to navigate through elements and attributes in an XML document.

_Snippet of an XML Structure:_
 
  ***Root***: Employees
  
  ***Child Elements***: Employee with Attribute "ID"
  
  ***Sub-Child Elements***: "FirstName", "LastName", "UserName", "Password", "Type"
  
```
<?xml version="1.0" encoding="utf-8"?>
<Employees>
   <Employee ID="1">
      <FirstName>Arnold</FirstName>
      <LastName>Baker</LastName>
      <UserName>ABaker</UserName>
      <Password>SoSecret</Password>
      <Type>Admin</Type>
   </Employee>
   <Employee ID="2">
      <FirstName>Peter</FirstName>
      <LastName>Pan</LastName>
      <UserName>PPan</UserName>
      <Password>NotTelling</Password>
      <Type>User</Type>
   </Employee>
</Employees>
```

Suppose Web Application has user authetication systems that takes username and password through user input and XPATH queries the xml snippet above to find the user.

```
C#:
String FindUserXPath;
FindUserXPath = "//Employee[UserName/text()='" + Request("Username") + "' And
        Password/text()='" + Request("Password") + "']";
```

Attacker can supply craft input in username and password field to interfer with the structure and bypass the authentication check.

Example of Atatcker Crafted Input:

```
Username: admin' or 1=1 or 'a'='a
Password: admin
```

The function to find user becomes

```
FindUserXPath = "//Employee[UserName/text()='admin' or 1=1 or
        'a'='a' And Password/text()='admin']"
```

Logically this is equivalent to:

```
//Employee[(UserName/text()='admin' or 1=1) or
        ('a'='a' And Password/text()='admin')]
```

In this logic, the attacker will be able to bypass authentication check since the check username has OR 1=1, which is always true and the password check is ignored because of the another or logic included by the attacker.

---

## Defenses against XPATH injections

  - User Input should be strictly validated before incorporating them into XPath queries.
  - In most cases, accept only short alphanumeric inputs.
  - Input containing meta characters " ' / @ = * [ ] ( and ) should be rejected.

  ### Fixing the vulnerability in the above code

  Single Quote  (‘) is used by attackers in the input fields to break out of username and password parameters. 
  So, we need to replace (‘) in input with ("'").

  ```
  FindUserXPath = "//Employee[UserName/text()='" + Request("Username").Replace("'","&apos;") + "' And
  Password/text()='" + Request("Password").Replace("'","&apos;") + "']";
  ```
---

## Reference
- OWASP:  https://owasp.org/www-community/attacks/XPATH_Injection
