# Login MC Safe Search (Sensitive Data Exposure)

**Solution:**

1. Try to log in with the username `admin@juice-sh.op` and password `test`.  
   → It will show "invalid password or username."  

2. Capture this request in Burp Suite while intercept is on.  

3. Send the login request to Repeater.  
    Change the username from `admin@juice-sh.op` to `mc.safesearch@juice-sh.op`.  
    Change the password from `test` to `Mr. N00dles`.  

4. The challenge will then be solved.  

-----------

**How does `mc.safesearch@juice-sh.op` come into play?**

By exploring publicly exposed endpoints and data leaks.  

Example endpoint:  

http
GET /rest/user/authentication-details/

This endpoint leaks a list of users, including email addresses, user IDs, and other information.

[
  {
    "email": "mc.safesearch@juice-sh.op",
    "user": "MC SafeSearch",
    ...
  },
  ...
]


