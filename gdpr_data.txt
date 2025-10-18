# GDPR Data Theft (Sensitive Data Exposure)

## Solution Steps

1. **Create a Dummy Account**  
   1. Register a new user with the following details:  
     a. Email: `asdf@asdf.com`  
     b. Password: `asdf`  
     c. Fill in other required profile details.

2. **Enable Burp Suite**  
   1. Start Burp Suite and configure the browser proxy.

3. **Place an Order**  
   1. Login with `asdf@asdf.com`.  
   2. Add a product to the basket with required details:  
     a. Address: `asdf`  
     b. Payment: Card number `1111111`, expiry month/year.  
   3. Place the order and complete payment.  
   4. A confirmation message *“Thank you for purchasing”* is displayed.  
   5. Click **Track your order** to see the order status.

4. **Inspect with Burp Suite**  
   1. In Burp HTTP history, locate the order request:  
     ```
     /rest/track-order/8716-bo7276761
     ```  
   2. Send this request to **Repeater**.  
   3. The response shows order details such as order ID and product, but the email address appears partially masked (`*`).

5. **Request Data Export**  
   1. Navigate in Juice Shop:  
     `Account → Privacy & Security → Request Data Export → JSON`.  
   2. Enable pop-ups for localhost if prompted.  
   3. Click **Request** again.  
   4. The complete information of the order is revealed, including:  
     a. Email ID  
     b. Order ID  
     c. Price  
     d. Product quantity  

6. **Test with Another User**  
   - Logout and create a new account with:  
     1. Email: `odmin@juice-sh.op`  
     2. Fill required details and register.  

7. **Access Previous User Data**  
   1. Login with `odmin@juice-sh.op`.  
   2. Without placing any order, navigate to:  
     `Account → Privacy & Security → Request Data Export → JSON`.  
   3. Solve the CAPTCHA and click **Request**.  
   4. The export reveals sensitive data from the **previous admin’s order**, showing email, order ID, and product details.  
   5. The email field displays `odmin@juice-sh.op`, but the associated data actually belongs to **admin’s earlier order**.

---

## Impact
This vulnerability demonstrates **GDPR Data Theft** where sensitive personal and order data of other users (including administrators) can be exposed through improper access controls on the data export feature.



