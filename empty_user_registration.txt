# OWASP Juice Shop – Empty User Registration

## Solution
1. Register for a new user ID by filling in the required details and clicking on **Register**.  
2. Capture the request in **Burp Suite** and send it to the **Repeater** (POST request).  
3. Delete the **username** and **password** fields from the request body and send the modified request.  
4. The server accepts the request and creates a user account even with empty fields.  

## Vulnerability
The registration form does not enforce required fields such as email, password, or security questions.  
The backend still accepts and creates a user account with missing or invalid information.  

**Root Cause:**  
This is a **server-side validation failure**. The server should validate inputs and reject any requests missing mandatory fields, but it fails to do so.  
