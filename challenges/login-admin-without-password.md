# 🔐 Challenge: Login Admin Without Password

**Category:** Broken Authentication  
**Status:** Solved  
**Difficulty:** Medium

---

## 🧪 Vulnerability: SQL Injection in Login

The login form allows SQL injection in the email field, which can be used to bypass password verification and log in as any user.

### Payload Used:
```sql
' OR email='admin@juice-sh.op'--

