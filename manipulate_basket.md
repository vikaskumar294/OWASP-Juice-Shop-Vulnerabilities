# OWASP Juice Shop Vulnerability Report

## Manipulate Basket (Broken Access Control)

**Vulnerability Location:** Basket / Shopping Cart API

### Steps to Reproduce

1. **Register as a user**  
   Create a new account in Juice Shop if not already registered.

2. **Log in**  
   Log in with the new user credentials.

3. **Add a product to the basket**  
   1. Open Burp Suite and intercept the request when adding a product to the basket.  
   2. Capture the POST request to `/api/Basket/items/` and send it to Repeater.

4. **Manipulate the basket**  
   1. Attempt sending the request with a modified product ID.  
   2. Example: change the product ID to `7` or another value.  
   3. Send the request and check the website; the manipulated product should appear in the basket.

5. **Test basket ID manipulation**  
   1. Copy the basket ID (e.g., `6`) and attempt to modify it in the request payload.  
   2. If sending results in an invalid basket ID error, try changing product ID and basket ID combinations:
     3. Change product ID: `7`, basket ID: `6` to `5`  
     4. Change basket ID: `6` to `7`  
   5. Send the request and verify if the basket shows the updated product.

### Test Credentials

1. **Email:** `test1@outlook.com`  
2. **Password:** `test@123`
