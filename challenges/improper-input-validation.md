# Challenge: Improper Input validation (OWSAP Juice Shop)

## Description
This challenge demonstrates how Improper Input Validation can be explioted to By intercepting a request before it reaches the server, we can alter form values.


## Steps to Reproduce
1. Navigate to the customer feedback page in OWSAP Juice Shop
2. Write any feedback in the provided form
3. Enable request interception (Using Burp Suite)
4. Submit the feedback form while the interception is active
5. Send the captured request to the repeater tool
6. Modify the rating field value (e.g: change it to 0 or any arbitrary number outside the allowed range)
7. Forward the modified request and observer that the system accepts it

## Vulnerabilities Exploited

** Privilege Escalation** -- Changing data to a value that should not be possible
** Data Leakage** -- Potential for exposing unintended system behaviour
** Broken Access Control**-- Server not validating the incoming rating value.
** Security Bypass**-- Circumventing client-side validation checks

## Mitgation Recommdations
1. Perform Server side validation for inputs, regardless of front-end restrictions
2. Implement whitelisiting for acceptable values
3. Log and monitor abnormal values for suspicious activity

## Takeway
Never trust data coming from client side. All validation must happen on the server, with strict rules on what is acceptable
