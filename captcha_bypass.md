# Captcha Bypass (Broken Anti-Automation)

**Affected application:** OWASP Juice Shop  
**Vulnerability category:** Broken Authentication / Broken Anti-Automation  
**Location:** Customer Feedback endpoint (`/api/Feedbacks/`)  
**Severity:** Medium (lab environment — capability to bypass anti-automation controls)

---

## Summary

A captcha/anti-automation control for the customer feedback flow can be bypassed by automating and replaying requests. The vulnerability allows automated submissions that should have been protected by anti-bot measures. This write-up documents a reproducible proof-of-concept performed against the OWASP Juice Shop test environment and suggests remediation steps.

> **Note:** The steps below were executed in a lab environment (OWASP Juice Shop). Do not attempt these techniques against production systems without explicit authorization.

---

## Proof of Concept (Steps to reproduce)

1. Navigate to the Customer Feedback page in the running OWASP Juice Shop instance and submit a feedback entry through the web form.
2. Capture the resulting request in Burp Suite. The request is a `POST` to `/api/Feedbacks/`.
3. Forward the captured request to Burp Repeater for analysis and replay.
4. Send the request to Burp Intruder:
   - In Intruder, configure the payload positions (target the appropriate fields in the POST body).
   - Set the payload type to **Null payload**.
   - Set the payload count to **15**.
5. Start the Intruder attack. In this lab instance, the attack will succeed and the Juice Shop challenge for bypassing anti-automation will be marked as solved.

_Observed behavior:_ Replaying and automating the captured feedback `POST` using repeated null payloads is sufficient to bypass the anti-automation protection in the Juice Shop lab.

---

## Impact

- Allows automated submission of feedback entries that should be blocked by captcha/anti-bot controls.
- In a real application, this could lead to spam, automated abuse, or bypass of application workflows that assume human interaction.

---

## Root cause (likely)

The anti-automation control is enforced client-side or via easily replayable tokens that are not tied to server-side state, session, or single-use validation. The server accepts identical or automated replays of the POST without sufficient server-side verification.