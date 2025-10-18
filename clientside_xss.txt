# Client-side XSS Protection (XSS)

**Affected application:** OWASP Juice Shop  
**Vulnerability category:** Cross-Site Scripting (Client-side)  
**Vulnerability location:** Login page / Customer Feedback / User registration endpoints  
**Severity:** Medium

---

## Summary

A client-side input validation flaw allows an attacker to inject HTML/JavaScript into user-supplied fields (email/feedback). By tampering with the registration or feedback request before it reaches the server, an attacker can persist or reflect a payload that executes in victims' browsers.

> **Note:** Execute only in your authorized lab environment (OWASP Juice Shop). Do not test this against systems without permission.

---

## Proof of Concept (Steps to reproduce)

1. Open the **Customer Feedback** page and try submitting a feedback entry with an iframe/script payload (this step shows the vector).  
2. Register a new customer account (use a valid email format). Have Burp Suite running. If the UI enforces email format, that is a client-side control.  
3. Capture the registration request (`POST /api/Users/`) in Burp Suite (Proxy → Intercept). You will see JSON with `email`, `password`, etc.  
4. Before forwarding the registration request, modify the `email` value to include the payload. Example payload:
   ```html
   <iframe src="javascript:alert('xss')">
5. Forward the edited request. If the application stores or reflects this field and later renders it without proper encoding/escaping, the payload will execute in the browser context of users who view the vulnerable content (e.g., admin or victim viewing feedback or user lists).