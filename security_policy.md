# Security Policy Challenge (OWASP Juice Shop)

## Solution:

1. Go to the OWASP Juice Shop Home page and search for `security.txt`.  
   a. Good practice is to search for `security.txt` and click on the first link:  
     **security.txt: Proposed standard for defining security policies**.

2. Check the frequently asked questions (FAQ) about `security.txt`, such as:  
   a. **Where should I put the security.txt file?**  
     b. For websites, the `security.txt` file should be placed under the `/.well-known/` path (`/.well-known/security.txt`) [RFC8615].  
     c. It can also be placed in the root directory (`/security.txt`) of a website, especially if the `/.well-known/` directory cannot be used for technical reasons, or simply as a fallback.  
     d. The file can be placed in **both locations** at the same time.

3. Copy this path `/.well-known/security.txt` and paste it in the URL like this:  
