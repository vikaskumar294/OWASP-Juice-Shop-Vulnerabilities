# OWASP Juice Shop — Login Jim

**Vulnerability:** Authentication Bypass (Improper Input Validation / SQLi-like injection)

**Vulnerability location:** Login page

## Summary
A crafted input in the username/password fields allows an attacker to authenticate as the user `jim@juice-sh.op` without knowing the real password. This is due to improper input handling on the login endpoint.


## Steps to reproduce
1. Open the Juice Shop login page.
2. In the **email/username** field enter: `jim@juice-sh.op`.
3. In the **password** field enter: `test`.
4. In the **email/username** field append the following payload (including the trailing characters) or enter exactly as shown if you can control the raw input (some UI flows require separate steps):
jim@juice-sh.op'--
5. Submit the login form.

**Result:** You will be logged in as `jim@juice-sh.op` and the challenge is marked as solved.

## Proof of concept (PoC)
1. Username: `jim@juice-sh.op'--`
2. Password: `test`

When the application concatenates or mishandles these inputs server-side, the appended `--` may comment out the rest of the SQL statement (or otherwise tamper with the authentication logic), allowing authentication bypass.


