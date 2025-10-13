# Upload size (Improper Input Validation)

**Project:** OWASP Juice Shop

**Vulnerability type:** Improper Input Validation / Broken Access Controls

**Location:** Complaint (file upload) feature

## Summary
The application incorrectly validates uploaded file contents and size checks can be bypassed by manipulating the multipart request body. This allows uploads that should be rejected by the server and completes the Juice Shop challenge for "Upload size".

## Impact
An attacker can upload files that exceed the intended size restrictions or bypass content-type checks. Depending on how the server processes uploaded files, this could lead to storage abuse, disclosure, or other unexpected behavior.

## Steps to reproduce (concise, reproducible)
1. Open the **Complaint** page and use the file upload control to attach a file (PDF or JPEG). Capture the upload request in Burp Suite.
2. Locate the captured request (POST `/file-upload`) and send it to Repeater.
3. Observe the request and response. Initially, sending the captured request returns **HTTP 204 No Content** (server accepted the request but did not store the file in the expected format).
4. On the complaint page, attempt to upload a file larger than 100 KB. The UI displays a message: **"can't upload more than 100kb"**.
5. In Burp Repeater, modify the multipart request body: remove the readable PDF content chunk and replace it with the contents of a different 100 KB PDF opened in a text editor (i.e., paste the unreadable binary/text representation). **Important:** Do not remove the multipart boundary termination line (for example: `------WebKitFormBoundaryhIpZVzlqIPVAWqvV--`) at the end of the body.
6. Send the modified request. The response should be **HTTP 204 No Content**, and the Juice Shop challenge for "Upload size" will be marked as solved.

## Notes
1. The issue is caused by insufficient validation of the uploaded payload at the server-side and reliance on client-side size checks or superficial content validation.
2. Keeping the multipart boundary intact is required for the server to parse the upload; altering only the content payload is sufficient to bypass size/content checks in this case.

