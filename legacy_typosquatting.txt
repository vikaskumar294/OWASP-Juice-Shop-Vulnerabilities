# Legacy Typosquatting (Vulnerable Components)

## Overview
**Typosquatting** (also called *URL hijacking*) is a technique where attackers register domain names that are visually or typographically similar to legitimate websites. These look-alike domains exploit human typing errors to intercept visitors, harvest credentials, deliver malware, or perform fraud.

**Examples:**
1. Real: `www.microsoft.com`  
2. Typosquat: `www.micosoft.com`, `www.micr0soft.com`

---

## Where it is used
1. **Phishing websites** — tricking users into entering credentials or sensitive information.  
2. **Malware delivery** — serving malicious installers or payloads.  
3. **Advertising / traffic fraud** — monetizing accidental traffic via ads or affiliate redirects.  
4. **Credential harvesting in corporate attacks** — mimicking internal services (e.g., `payrol1.company.com`) to capture employee logins.  

---

## Goal
Typosquatting exploits **human error** (mistyped URLs). Common attacker goals include:
1. Stealing sensitive data (passwords, banking info, personal data).  
2. Spreading malware.  
3. Generating revenue (ads, scams, affiliate fraud).  
4. Damaging the reputation of the target brand.  

---

## OWASP Juice Shop — Challenge: Legacy Typosquatting (Vulnerable Components)

### Description
This challenge demonstrates a legacy vulnerable component that references a typosquatting package. By retrieving a backup package manifest, you can identify the malicious/misspelled component name and use it to solve the challenge.

---

### Solution Steps
1. Launch Juice Shop locally and navigate to the app (`http://localhost:3000`).  
2. In the browser, switch the protocol to `ftp` and locate the `package.json.bak` file.  
3. Append `%2500.md` after `package.json.bak`. Example:  

ftp://localhost/path/to/package.json.bak%2500.md

4. Download the file. It contains package metadata (name, version, homepage, keywords, contributors, author).  
5. Inspect the file for suspicious or misspelled package names (typosquatting components).  
6. In this challenge, the identified component is **`epilogue-js`**.  
7. Go to the **Score Board** page → open the Typosquatting challenge → follow the link to the feedback page.  
8. Enter the typosquatting component name (`epilogue-js`) in the comments section and submit.  
9. The challenge is marked as **solved**.  

---

### Key Indicators of Typosquatting in Package Files
1. Misspelled or look-alike names.  
2. Irrelevant or suspicious homepage links.  
3. Contributors or keywords inconsistent with the project.  
4. Packages imitating legitimate dependencies with small typos.  

---

## Summary
1. Download `package.json.bak%2500.md` via FTP.  
2. Inspect the manifest for a typosquatting component.  
3. Submit the discovered package (`epilogue-js`) in the feedback page.  
4. Challenge solved.  
