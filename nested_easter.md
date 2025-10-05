# OWASP Juice Shop Vulnerability: Nested Easter Egg (Cryptographic Issues)
---
## Description
This challenge involves finding a hidden easter egg file and decoding a cryptographic message to reveal a path in the application.
---
## Solution Steps

1. Navigate to the URL `/ftp`. You will see a file named `easter_egg`. Click on it; initially, you will encounter a **403 Forbidden** error.  
2. Append `%2500.md` to the URL and press **Enter**. A message will pop up. Open it in **Notepad** or **Visual Studio** to view its content, which contains an unreadable format string.  
3. Copy the string and open **CyberChef**. Paste the string and use **Base64 decode** to extract an intermediate output.  
4. Apply **ROT13** encryption in CyberChef by dragging it into the recipe. ROT13 rotates each character by 13 positions.  
5. The output will now make more sense and reveal a readable path.  
6. Copy the resulting path and append it to the URL in the browser. Accessing this URL will complete the challenge.
---
## Notes
1. The challenge teaches basic cryptographic transformations including **Base64 decoding** and **ROT13 rotation**.
2. Carefully following the sequence of transformations is essential to reveal the hidden path.
