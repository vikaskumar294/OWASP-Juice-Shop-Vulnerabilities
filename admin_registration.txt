# Admin Registration

**Vulnerability:** Improper Input Validation  

**Solution:**  
1. Go to the register page and register using `admin@123.outlook.com`.  
2. Capture this request in Burp Suite (`POST /api/users/`).  
3. Send it to Repeater. By default, the role is set as `"customer"`.  
4. Modify the request:  
   - Change the email to `"admin1@123.outlook.com"`  
   - Under `"passwordRepeat"`, add `"role": "admin"`  
5. Send the request. The response will now show `"role": "admin"`.  
6. Login with the updated email (`admin1@123.outlook.com`). You will now have admin-level permissions.  
