# Password Strength (Broken Authentication)

## Solution

1. Attempt to log in using the credentials:  
   **Username:** admin@juice-sh.op 
   **Password:** test
   The application responds with *invalid email or password*.

2. Capture the login request using **Burp Suite** and forward it to **Intruder** for further testing.

3. Use a password list for brute-force attempts. A reliable source is:  
   [SecLists - Common Credentials (best1050.txt)](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/best1050.txt)

4. Copy and load the password list into Intruder, then start the attack.  

5. Once a matching password is found for the username, identify the correct request and use it to successfully log in.  
