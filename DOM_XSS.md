#  OWASP Juice Shop --- DOM XSS Challenge

## Vulnerability
**Type:** DOM-based Cross-Site Scripting (DOM XSS)  
**Cause:** The search bar input is processed by client-side JavaScript without sanitizing or escaping user input.  
**Risk:** Attackers can inject malicious scripts into the page, leading to cookie theft, phishing, or unauthorized actions.


##  How I Solved It
1. Entered the payload in the search bar:
   ```html
   <iframe src="javascript:alert(`xss`)">

2. Opened Developer Tools ---> inspected the DOM
3. Found my <iframe> element directly inserted into the page without sanitization
4. The payload executed, displaying the alert('xss') popup confirming the DOM XSS vulnerability.





## Takeaways

1. DOM XSS occurs entirely on the client side when JavaScript handles untrusted input insecurely.

2. Always sanitize and escape user input before inserting it into the DOM.

3. Use safe DOM manipulation methods (textContent instead of innerHTML).

4. Combine manual testing with browser DevTools to detect and verify vulnerabilities.