# Deprecated Interface (Security Misconfiguration)

## Solution

**Vulnerability Location:** Complaint Section  

### Steps to Reproduce

1. Navigate to the **Complaint** section and select **Choose File** to check the supported file extensions (e.g., PDF, JPEG).  
2. Open **Developer Tools** and inspect `main.js`. Search for the terms `zip`, `application/zip`, or `application/x-zip-compressed`.  
3. Create a `test.xml` file and upload it using the **Choose File** option.  
4. Enable **Intercept** in Burp Suite.  
5. Enter any message in the complaint form and submit it.  
6. In Burp Suite, observe the `test.xml` file being processed. Click **Forward** and then disable Intercept.  
7. Review the **HTTP History** in Burp Suite. The uploaded file appears as an HTML file, indicating a security misconfiguration.  

