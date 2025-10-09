# OWASP Juice Shop Challenge: Repetitive Registration

## Challenge Description
The **Repetitive Registration** challenge in OWASP Juice Shop requires exploiting the application’s weak registration and password reset mechanism. By registering or resetting accounts multiple times, it becomes possible to interfere with existing users or gain unauthorized access.

---

## Steps to Solve

### 1. Create a New Account
- Register a new account with the following details:
  - **Email:** `abcd@juice.shop.com`
  - **Password:** `testtest`

---

### 2. Reset the Password
- Reset the password of the created account:
  - **New Password:** `test`

---

### 3. Target Existing Accounts
- Use the password reset flow to reset passwords of existing accounts:
  - **Admin Account:**  
    - **Email:** `admin@juice-sh.op`  
    - **Password (after reset):** `test@123`  

---

## Outcome
- Successfully created a new account.  
- Exploited the weak reset process to set a known password for an existing account (`admin@juice-sh.op`).  
- Gained unauthorized access, solving the challenge.  

---

## Mitigation (Best Practices)
To prevent this type of vulnerability:
1. Enforce **unique email validation** during registration.  
2. Implement **secure password reset with verification tokens**.  
3. Ensure password reset links are **time-bound and single-use**.  
4. Add **multi-factor authentication (MFA)** for sensitive accounts.  
