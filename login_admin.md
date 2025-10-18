# Challenge: Login Admin

## Solution
1. Start **Burp Suite** and enable interception.
2. Try logging in with:
   Username: `admin`
   Password: `test`
   The login attempt fails.
3. Capture the request to `/rest/user/login`.
4. Send the request to **Repeater**.
5. Modify the `email` field with the following SQL injection payload:

6. Send the modified request.
7. Login succeeds, granting access as the **Admin user**.

## Vulnerability Type
 **SQL Injection (Authentication Bypass)**

## Impact
 Attackers can gain unauthorized access to privileged accounts (e.g., Admin).
 Compromises confidentiality, integrity, and availability of the application.

## Mitigation
 Use **parameterized queries** or **prepared statements** to handle database inputs safely.
 Apply **strict input validation and sanitization** for user-supplied data.
 Limit database account privileges using the **principle of least privilege**.
 Implement monitoring and alerting for suspicious login activities.
