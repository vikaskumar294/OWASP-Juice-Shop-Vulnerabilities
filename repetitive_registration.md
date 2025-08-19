# OWASP Juice Shop – Repetitive Registration

## Vulnerability
**Improper Account Registration Validation.**  
The application fails to prevent duplicate or closely related accounts from being registered with the same or similar email addresses. This weakness allows attackers to repeatedly register accounts for existing users or administrators by slightly modifying the email pattern.

---

## Vulnerability Location
- The issue is located in the **user registration process** (`/api/Users/`).  
- Juice Shop does not properly validate uniqueness of certain email addresses or enforce strict domain rules.  
- This allows the creation of duplicate or closely resembling accounts, including accounts that impersonate administrative users.

---

## Steps to Reproduce
1. Navigate to the **Register** page in Juice Shop.  
2. Create a new user account with the following details:  
   - **Email:** `abcd@juice.shop.com`  
   - **Password:** `testtest`  
   - Confirm registration.  
3. Now, attempt to **reset the password** for that account using the “Forgot Password” functionality.  
   - Enter email: `abcd@juice.shop.com`  
   - Set a new password: `test`.  
4. Next, try creating or modifying accounts using **similar email patterns** that Juice Shop mistakenly accepts:  
   - **Email:** `admin@juice-sh.op`  
   - **Password:** `test@123`  
5. The application allows these registrations even though they bypass intended uniqueness and security checks.  
6. Once completed, the **Repetitive Registration** challenge is marked as solved.

---

## Impact
- Attackers can register accounts using **confusingly similar email addresses** to trick other users or administrators.  
- This can lead to **account impersonation**, phishing, or privilege escalation attempts.  
- By leveraging password reset functionality, attackers may gain access to accounts they should not control.  
- In real-world applications, such weaknesses can be abused to compromise critical accounts or flood systems with fake accounts.

---

## Takeaways
- Always enforce **strict uniqueness checks** on email addresses during registration.  
- Normalize email addresses (strip dots, handle case sensitivity, and validate domains properly).  
- Prevent registrations that attempt to spoof existing domains or administrative accounts.  
- Implement rate-limiting and monitoring to detect suspicious repeated registration attempts.  
- Real-world apps should use verification mechanisms (e.g., confirmation emails, domain checks) to prevent fake or duplicate accounts.

---
