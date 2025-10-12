Confidential Document (Sensitive Data Exposure)
Page: About Us

Steps:

Click on the highlighted link that allows downloading a file (legal.md).

Capture the request in Burp Suite for legal.md.

Send the request to the repeater and modify it by replacing legal.md with acquisition.md.

Send the modified request. In the response, you will see the contents of acquisition.md.

Vulnerabilities Observed:

Improper access control on unprotected files (Sensitive Data Exposure via direct object access).

Juice Shop exposes sensitive documents (like .md, .bak, or hidden files) under /ftp/ or similar paths without authentication or access checks.

Takeaways / Learning Points:

Always validate and restrict access to files on the server to prevent unauthorized downloads.

Avoid exposing sensitive documents publicly without proper authentication.

Understand how Direct Object Reference (IDOR) vulnerabilities work and how attackers can enumerate files.

Tools like Burp Suite can help identify sensitive data exposure in web applications.