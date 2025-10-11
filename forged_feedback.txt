# Forged Feedback (Broken Access Control)

## Solution
1. Navigate to the **Feedback Form** in OWASP Juice Shop.  
2. Turn on the proxy and capture the request in **Burp Suite**.  
3. Send the request to the **Repeater** tab.  
4. Modify the `UserId` field, e.g., change from `UserId: 1` to `UserId: 4`.  
5. After modification, the feedback appears as if it was submitted by another user (e.g., User 4, "Jeff Bezo's"), giving a fake rating of 1.  

This could mislead users and create **trust issues** with the product reviews.

---

## What’s the Vulnerability?
This issue is a **Broken Access Control** vulnerability — specifically **Insecure Direct Object Reference (IDOR)**.  

- **Direct Object Reference** → The system lets the client decide which object (user account, order, or review) to act on, using an ID.  
- **Insecure** → The server fails to validate whether the client is authorized to act on that object.  

### In the Juice Shop case:
- The server accepts `"UserId": 4` in the feedback request.  
- It does **not verify** that UserId 4 actually belongs to the logged-in user.  
- As a result, an attacker can submit feedback **impersonating another user**.

---
