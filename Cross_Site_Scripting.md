# Cross Site scripting (XSS)

## What is XSS?

    It is a Web Application vulnerability that allows an attacker to compromise the interactions
    that users have with the application.

    It allows attackers to circumvent the same origin policy, which is designed to segregate
    different websites from each others.

---

## How does XX work?

    It works by manipulating the vulnerable website so that it returns malicous javascript to the users.

    When malicous code executes in user's browser, the attcker can fully compromise their interaction with the application.

## Types of XSS

    - Reflected XSS
        The script is reflected off the server, usually via a URL or query parameter.
    - Stored XSS
        The malicious script is permanently stored on the server (e.g., in a database or comment field).
    - DOM-based XSS
        The vulnerability exists in client-side JavaScript that dynamically updates the page without proper handling of user input.
---
## proof of Concept

    Popular Payloads to confirm existence of xss type of vulnerabilities

    - `<script>alert(1)</script>`
    - `"><img src=x onerror=alert(1)>`
    - `<svg/onload=alert(1)>`

---

## How to prevent XSS

    - Filter input on arrival.
    - Encode data on output.
    - Use appropriate response headers.
    - implement Content Security Policy.

---

## Reference

    https://portswigger.net/web-security/cross-site-scripting
