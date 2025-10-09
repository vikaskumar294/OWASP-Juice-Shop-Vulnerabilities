# Five‑Star Feedback — Broken Access Control

**Vulnerability:** Broken Access Control

**Challenge / Location:** Five‑Star Feedback (`/#/administration`)

## Explanation

The application does not properly restrict access to the administration page. Any user can directly access the admin route and perform actions that should only be allowed for administrators.

## Steps to Reproduce

1. Log in to Juice Shop with any normal user account.
2. In the browser, manually go to:

   ```
   http://<JUICE_SHOP_HOST>/#/administration
   ```
3. The administration panel loads even though you are not an admin.
4. From here, locate the 5‑star rating in the feedback list and delete it.

## Impact

* Normal users can perform admin actions.
* Feedback ratings can be manipulated.

## Fix

* Add proper server‑side authorization checks to ensure only admin users can access `/#/administration` and related API endpoints.
* Use role‑based access control to prevent unauthorized actions.

## Commit Message Example

```
docs: add simple writeup for Five-Star Feedback (Broken Access Control)
```
