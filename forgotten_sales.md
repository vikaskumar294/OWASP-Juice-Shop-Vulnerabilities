# OWASP Juice Shop Challenge: Forgotten Sales Backup

## Challenge Overview
The *Forgotten Sales Backup* challenge involves exploiting improperly stored backup files that developers have left accessible on the server. By identifying and bypassing access controls, sensitive information such as source code, user emails, and JavaScript logic can be retrieved.

---

## Solution Steps

1. **Navigate to the FTP directory**
   1. Type `ftp` in the URL bar.
   2. A page with folders will appear.  
   3. Locate `package.js` and then access `coupons_2013.md.bak`, which indicates a developer backup file (`.bak` extension).

2. **Encountering a 403 Forbidden Error**
   1. When opening the `.bak` file directly, the server returns a **403 Forbidden** error.  
   2. Append `%00.md` to the URL and press **Enter**.

3. **Handling the 400 Bad Request Error**
   1. The appended `%00.md` leads to a **400 Bad Request** error.  
   2. Open **CyberChef** and paste `%00`.  
   3. Select **URL Encode** → this converts `%00` into `%2500`.

4. **Download the Backup File**
   1. Replace `%00` with `%2500` in the URL → `%2500.md`.  
   2. The file downloads successfully.  
   3. Opening it in a text editor reveals **source code, user email addresses, and JavaScript code**, confirming the challenge completion.

---

## Key Takeaways
1. Backup files with `.bak` extensions often expose sensitive information.  
2. Encoding tricks (`%00` → `%2500`) can bypass input validation filters.  
3. Always ensure backups are stored securely and never exposed in public directories.  

---
