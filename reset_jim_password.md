# Reset Jim’s Password (Broken Authentication)

**Affected application:** OWASP Juice Shop
**Vulnerability category:** Broken Authentication
**Location:** Password reset endpoint (`/rest/user/reset-password`)
**Severity:** Medium

---

## Summary

The password reset function for user **Jim** can be exploited by guessing or brute-forcing the answer to his security question. Once the correct answer (`Samuel`) is found, an attacker can reset his password and log in.

---

## Proof of Concept (Steps to reproduce)

1. Go to the login page → click **Forgot Password**.
2. Enter `jim@juice-sh.op`, provide any temporary answer, and set a new password. It will return *Wrong answer to security question*.
3. Capture the request in Burp Suite (POST `/rest/user/reset-password`).
4. Send the request to Intruder and place a payload marker on the `answer` value.
5. Use a wordlist of common names as payloads and run the attack.
6. The correct answer is `Samuel`. Submitting it allows you to reset Jim’s password.
7. Log in as `jim@juice-sh.op` with the new password.

---

## Impact

* Unauthorized reset of Jim’s password.
* Demonstrates the weakness of security-question–based authentication.

---

## Recommended Remediation

1. Avoid using security questions for password resets.
2. Use email or token-based password recovery.
3. Apply rate-limiting and monitoring to reset attempts.

---

## Suggested filename

`reset-jims-password_broken_authentication.md`

---



