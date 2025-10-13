# OWASP Juice Shop Vulnerability Write-up

## Upload Type (Improper Input Validation)

**Vulnerability Location:** Compliant feature  

### Solution Steps:

1. Go to the compliant box and write a test message in the message feature. Upload a PDF file using the upload feature and capture that request in Burp Suite.  
2. Capture the request: `POST /file-upload HTTP/1.1` and send it to the Repeater.  
3. On the request side, you will see a non-format PDF. Click **Send**. After sending, the response shows `204 No Content`.  
4. On the request side, delete the unreadable PDF content. Open a JPG file in Notepad, copy its unreadable content, and paste it in the request body in Burp Suite. **Do not remove** this line at the end:  
------WebKitFormBoundaryhIpZVzlqIPVAWqvV--
5. Change the file extension in the request from `.pdf` to `.jpg`, for example:  
filename="VikaskumarCSE (12).jpg"
Content-Type: application/jpg
6. Click **Send**. The response will show `204 No Content`, and the challenge will be solved.  
