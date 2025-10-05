# Challenge: Admin Section (Broken Access Control)

## Description
This challenge exploits **Broken Access Control** in OWASP Juice Shop.  
The application exposes an admin panel that is not properly protected, allowing unauthorized users to access sensitive features.

## Steps to Reproduce
1. Launch Juice Shop locally (`http://localhost:3000`).
2. Navigate directly to the following URL:
http://localhost:3000/#/administration
3. Observe that the **Administration Panel** is accessible without requiring proper admin authentication.

## Impact
Unauthorized access to admin functionalities.
 Potential to view and manage sensitive data.
 Demonstrates lack of role-based access control (RBAC).

## Mitigation
 Implement proper **role-based access control** checks.
 Restrict access to `/administration` routes for non-admin users.
 Apply server-side authorization instead of relying only on client-side checks.
