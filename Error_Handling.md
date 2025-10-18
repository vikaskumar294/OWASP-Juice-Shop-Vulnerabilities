# OWASP Juice Shop – Error Handling (Security Misconfiguration)

## Vulnerability
- **Type:** Security Misconfiguration – Detailed Error Handling  
- **Cause:** The application exposes detailed internal error messages when an invalid or unexpected API path is accessed.  
- **Risk:** Revealing stack traces or internal error details can give attackers valuable information about the application's internal structure and technologies.

---

## How I Solved It
1. Opened the OWASP Juice Shop product page, clicked on a product, and then closed it.
2. In Burp Suite, located the network request:

GET /rest/products/1/reviews

3. Sent this request to the **Repeater** and clicked **Send** to confirm it worked normally.
4. Modified the endpoint to a random non-existent path:

GET /rest/products/test/reviews

5. Sent the request again.  
6. The application returned an **Internal Server Error (500)** and displayed the word `test` in the response, along with a detailed error message and stack trace.



---

**Result:** Identified a Security Misconfiguration in OWASP Juice Shop where accessing an unexpected API path exposed detailed internal error messages.
