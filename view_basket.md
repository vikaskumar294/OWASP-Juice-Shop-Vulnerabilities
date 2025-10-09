View Basket (Broken Access Control)
***********
Procedure:

Log in as user admin@juice-sh.op with password admin123.

Go to the Basket page.

Open browser developer tools → Application tab → Session Storage.

Locate the bid value and change it to another number.

Refresh the page. The basket now shows items from a different user.

************
Explanation:
This works because the application relies on the client-side bid stored in session storage to identify which basket to display. The server does not check whether the modified bid actually belongs to the logged-in user. As a result, by simply changing this value, one user can access another user’s basket.

**********
Impact:

Unauthorized access to other users’ baskets.

Exposure of sensitive shopping data.

Potential for manipulation of another user’s items.

Fix:
The server should enforce strict ownership checks. Basket access must be tied to the authenticated user session, not a client-controlled ID.