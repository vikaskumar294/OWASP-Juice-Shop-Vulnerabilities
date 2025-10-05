# Misplaced Signature File (Sensitive Data Exposure)

## Overview
This document explains the **Misplaced Signature File** vulnerability in OWASP Juice Shop, which allows sensitive data exposure through improper file handling and null-byte injection.

---

## Summary
The Juice Shop application restricts access to files ending with `.yml`, but allows `.md` or `.pdf`. By exploiting this behavior with a null byte injection, attackers can bypass the restriction and access the sensitive `suspicious_errors.yml` file.

---

## Affected Resource
`/ftp` → Contains the misplaced file `suspicious_errors.yml`

---

## Severity Level
**Medium to High (Sensitive Data Exposure)**  
Leaking internal configuration files or signature data can lead to exposure of sensitive information like tokens, paths, or system details.

---

## Steps to Reproduce
1. Navigate to the `/ftp` page in the OWASP Juice Shop application.  
2. Use **Burp Suite** to intercept requests.  
3. Attempt to access the file `suspicious_errors.yml`. The response returns **403 Forbidden**, allowing only `.md` and `.pdf` extensions.  
4. Modify the request using a null byte injection to trick the file extension check:

suspicious_errors.yml%00.md

If the application decodes twice, use double encoding:

suspicious_errors.yml%2500.md



5. Send the modified request through **Burp Repeater**. The server interprets the `%00` as a null byte and returns the original `.yml` file.

---

## Technical Explanation
- Null bytes (`\x00`) act as **string terminators** in C-based systems. When the server checks the file extension using string comparison but reads the file using lower-level I/O functions, it stops processing at the null byte, resulting in the original `.yml` file being accessed.  
- The `%2500` encoding ensures that the `%00` sequence passes through URL decoding layers safely.  
- This issue arises from **improper file extension validation** and lack of canonicalization.

---

## Example Request

### Burp Repeater Example
GET /ftp/suspicious_errors.yml%2500.md HTTP/1.1
Host: juice-shop-host
User-Agent: Mozilla/5.0
Accept: /
Connection: close

---
### Impact

If successful, an attacker could retrieve sensitive internal configuration files. This may include:

1. Application logs or YAML configs
2. File paths or developer emails
3.Debugging or signing information