# OWASP Juice Shop — Forgotten Developer Backup

**Challenge:** Forgotten Developer Backup (process done but not showing in the page)

## Summary
A developer backup file (`package-lock.json.bak`) exposed in an FTP-style directory listing can be retrieved by bypassing naive input filtering via URL encoding. The backup file contains developer information and JavaScript source, confirming sensitive data leakage. This document describes the reproduction steps, explanation of the payload, impact, and remediation. Save this file as `Forgotten-Developer-Backup.md` for your GitHub repository.

---

## Target
1. OWASP Juice Shop (training application)
2. Endpoint: FTP-style directory listing accessible via browser

---

## Vulnerability type
1. Exposed developer backup file
2. Information disclosure due to improper file handling and input validation

---

## Preconditions
1. Access to the application where an FTP-style directory listing is reachable via browser.
2. A browser and an intercepting proxy (Burp Suite or similar) to assist with encoding.

---

## Reproduction steps (clean & reproducible)
1. In your browser, type `ftp` in the application URL to reach the FTP-style directory listing. The page displays folders and files.  
2. Navigate into the folder containing `package-lock.json.bak` (for example under `package.js`) and click the `package-lock.json.bak` link.  
3. The server responds with `403 Forbidden`, indicating the file exists but direct access is blocked.  
4. Append `%00.md` to the end of the file URL and request it. The server returns `400 Bad Request`.  
5. Open Burp Suite → Decoder and URL-encode the `%00` payload. The encoded sequence becomes `%25%30%30` (this is the encoding of the literal string `%00`).  
6. Replace `%00.md` with `%25%30%30.md` in the URL and request the resource. The server returns the file for download.  
7. Open the downloaded file in a text editor (for example, Notepad). You will find JS source fragments and developer email(s) inside, confirming sensitive information disclosure.

---

## Why the payload works
1. `%00` represents a null byte (string terminator in some languages). Some server-side code or file APIs may treat a null byte as terminating the string used for filtering while the filesystem still interprets the full filename.  
2. Sending `%00` directly may be normalized or rejected by the server. Encoding the percent sign (`%` → `%25`) yields `%25%30%30`, which bypasses naive filters and allows retrieval of the `.bak` file.

---

## Proof of concept (sanitized example)
The backup file typically resembles a `package-lock.json` or JavaScript artifact and may contain developer metadata:

```json
{
  "name": "juice-shop-backup",
  "version": "1.0.0",
  "author": "developer@example.com",
  "dependencies": { /* ... */ }
}
