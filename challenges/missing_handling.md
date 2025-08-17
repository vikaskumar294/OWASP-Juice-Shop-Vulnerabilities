## 5. Missing Encoding (Improper Input Validation)

**Vulnerability Type:** Input Validation / URL Encoding Issue  
**Vulnerability Location:** Photo Wall Page  

### Steps to Reproduce & Solution

1. On the Photo Wall page, one of the pictures is not displaying correctly.  
2. Open **Developer Tools** → Inspect the `img` tag.  
   - The issue is caused because the `#` symbol in the image URL is not properly encoded (it splits the URL).  
3. To fix this:  
   - Open **CyberChef** in Chrome.  
   - Search for **URL Encode**.  
   - Encode the `#` symbol.  
   - Copy the encoded value and replace the `#` in the image URL.  
4. The image now renders correctly, resolving the issue.  

### Key Takeaways

- Always encode special characters in URLs (`#`, `?`, `&`, etc.) to prevent broken links or improper rendering.  
- Improper input validation can lead to functional bugs and potential security risks.  
- Developer tools and utilities like **CyberChef** are effective for diagnosing and fixing encoding issues.  
- Secure coding practices require **proper encoding/escaping** of user input before processing.  
