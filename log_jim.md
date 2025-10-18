# Login Jim — Authentication Bypass

## Overview
1. This challenge demonstrates an authentication bypass vulnerability in the login functionality of the OWASP Juice Shop application.  
2. The goal of the challenge is to log in as another user (Jim) without knowing his actual password by exploiting improper handling of input on the login page.

---

## Solution Steps

1. **Login as Admin**
   a. Log in to the website using the admin account.
   b. Go to the product reviews section.
   c. Check the reviews for a product, for example, the *Banana Juice* product.
   d. You’ll find a review posted by a user named **Jim** with the email ID **jim@juice-sh.op**.

2. **Logout**
   a. Log out from the admin account.

3. **Bypass Login**
   a. Go to the login page.
   b. In the **Email** field, enter:  
     ```
     jim@juice-sh.op'--
     ```
   c. In the **Password** field, type:  
     ```
     test
     ```
   d. Click **Login**.

4. **Challenge Solved**
   a. You’ll be successfully logged in as the user **Jim**, meaning the authentication bypass worked and the challenge is completed.

---

## Explanation
1. The login functionality in this challenge is vulnerable to **SQL Injection**.  
2. By entering a specially crafted input (in this case, adding `'--` after the email), the query that checks login credentials is manipulated to ignore the password verification part.  
3. As a result, the application logs in the attacker without validating the password.

This occurs because the input is not properly sanitized before being included in a SQL query. The `'--` sequence is used to comment out the rest of the SQL statement, bypassing authentication logic.

---

## Conclusion
1. This challenge shows how improper input handling can lead to authentication bypass using SQL Injection.  
2. By implementing secure coding practices, such as input sanitization and parameterized queries, such vulnerabilities can be prevented effectively.




