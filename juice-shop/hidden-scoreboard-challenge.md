# 🛡️ Juice Shop Challenge: Hidden Score Board

## 🧠 Challenge Name:
**"Find the Score Board"**

## 🎯 Objective:
Access the hidden `/#/score-board` page in the OWASP Juice Shop.

---

## 🔍 How I Solved It

### 1. Clue from Burp Suite:
I intercepted a GET request to:
GET /api/Challenges/?name=Score%20Board


It hinted that a Score Board feature existed.


### 2. Looked into JavaScript Files:
I opened DevTools → Sources → `main.js` → searched `score-board`.

I found a route definition like:
```js
{ path: 'score-board', component: ScoreBoardComponent }
