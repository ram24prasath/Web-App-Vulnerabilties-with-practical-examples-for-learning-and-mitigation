# SQL Injection (SQLi)

## What is it?

    SQL Injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. It typically allows attackers to view data they are not supposed to retrieve, and in severe cases, modify or delete data, and even execute administrative operations.

---

## How does it Occur?

    SQL Injection occurs when user input is directly embedded into an SQL query without proper validation or sanitization. This enables an attacker to inject malicious SQL statements into a query, potentially gaining unauthorized access to database information.

---

## How to find/detect it?

    Detecting SQL injection by manual systematic set of tests.

    1. The Single Quote Character ``` ' ``` and look for internal server error.
    2. Try injecting ``` ' OR 1=1 -- ``` , ``` ' OR 'a'='a ``` , or ``` '; DROP TABLE users; -- ``` into input fields.
    3. Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.

## How to prevent SQL injection.

    - Use Parameterized Queries / Prepared Statements
    - Sanitize and Validate User Inputs
    - Use Object Relational Mappers (ORMs)
    - Limit Database Privileges
    - Deploy Web Application Firewall (WAF)

## Example of SQLi

    Vulnerable Python Example:
        ```
        user = request.GET['username']
        query = "SELECT * FROM users WHERE username = '" + user + "'"
        cursor.execute(query)
        ```
    
    Secure/ Fixed Code:

        ```
        user = request.GET['username']
        cursor.execute("SELECT * FROM users WHERE username = %s", (user,))
        ```

## reference and further readings

    https://portswigger.net/web-security/sql-injection
