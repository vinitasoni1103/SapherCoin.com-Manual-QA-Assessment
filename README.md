# SapherCoin.com-Manual-QA-Assessment
 
> **Company:** Sapher AllHeart Pvt Ltd  
> **Testing URL:** https://app.saphercoin.com/sign-up  
> **Blockchain Explorer:** https://explorer.sapherchain.com/  
> **Type:** Real-world QA assessment assigned by company  
> **Duration:** 1 week  
> **Tester:** Vinita Soni  
 
---
 
## 📌 Project Overview
 
SapherCoin is a blockchain-based crypto wallet application. This repository contains all QA deliverables from a manual testing assessment assigned by Sapher AllHeart Pvt Ltd, covering the full user journey from account registration to blockchain transaction verification.
 
---
 
## 🎯 Testing Scope
 
| Module | Description |
|---|---|
| Account Creation | Registration flow, email verification, login/logout |
| Wallet | Wallet address display, copy, balance accuracy |
| Coin Transfer | Sending coins between accounts, balance deduction/credit |
| Blockchain Explorer | Transaction verification on-chain |
 
---
 
## 📁 Repository Structure
 
| File | Description | Link |
|---|---|---|
| `README.md` | Project overview and findings summary | — |
| `Test_Cases.xlsx` | 40 structured test cases across 4 modules | https://docs.google.com/spreadsheets/d/1atrm8JNFFBidKaq3SJKZWSgt0KU4Phib1j3KBuyGVGU/edit?gid=73569990#gid=73569990|
| `Bug_Report.xlsx` | 14 bugs with severity, steps, expected vs actual | https://docs.google.com/spreadsheets/d/1o-XqQBIeKvkq0GDtLJCkXhkyiD2tn6868hK_ao2eOag/edit?gid=0#gid=0|
```
 
---
 
## 🐛 Bug Report Summary
 
**Total Bugs Found: 14**
 
| Severity | Count |
|---|---|
| 🔴 High | 7 |
| 🟡 Medium | 6 |
| 🟢 Low | 1 |
 
### Notable Bugs
 
**BG-011 – Authentication Bypass via Phone OTP** *(High/High)*  
Account becomes fully accessible via Phone OTP without enforcing email verification. Because the registration email is permanently uneditable post-signup, a typo during registration permanently locks the user out of password recovery — a critical security and UX flaw.
 
**BG-007 – Password Reset Link Hijacked by Active Session** *(High/High)*  
When a session is active on Device A, clicking the password reset link on Device A (received after initiating reset from Device B) bypasses the reset form entirely and redirects to an internal dashboard page. Root cause: conflict between active session cookies and the reset token verification route.
 
**BG-012 – Inbound Transactions Never Recorded in History** *(High/High)*  
Received coins correctly update the wallet balance but the transaction history shows "No Transactions Yet" for all inbound credits across all tested accounts — a complete ledger discrepancy.
 
**BG-013 – Undisclosed Gas Fee Deducted Without UI Warning** *(Medium/High)*  
Transferring 1.00000 SAPH results in a deduction of 1.00042 SAPH with no itemized fee breakdown shown before or after the transaction. Users have no way to anticipate the actual cost.
 
**BG-010 – Raw Backend Error Exposed to User** *(High/High)*  
Entering an international phone number during signup triggers a raw infrastructure error toast: *"Failed to send OTP from all providers"* — leaking internal system logic to end users instead of a clean user-friendly message.
 
---
 
## 🧪 Test Cases Summary
 
**Total Test Cases: 40**
 
| Module | Count |
|---|---|
| Account Creation | 10 |
| Wallet | 6 |
| Coin Transfer | 13 |
| Blockchain Explorer | 11 |
 
Test cases include: Test ID, Preconditions, Step-by-step instructions, Expected Result, Actual Result, Status, Priority, Severity, and Test Type (Functional / Negative).
 
---
 
## 🛠️ Tools Used
 
| Tool | Purpose |
|---|---|
| Browser DevTools | Console error inspection, network tab analysis |
| Microsoft Edge / Chrome | Cross-browser testing |
| Postman | API behaviour observation |
| Excel / Google Sheets | Test case and bug report documentation |
 
---
 
## 💡 Key Observations
 
- The application has a **critical authentication design flaw** where phone OTP login completely bypasses email verification, creating permanent unrecoverable accounts on typo emails
- **Transaction history is unreliable** — inbound credits update balances but leave no ledger trace, making the history module non-functional for receivers
- **Security hygiene gaps** exist including raw error exposure, weak password acceptance, and insecure URL structures exposing backend terminology (`/database/transactionhistory`)
- **Gas fees are silently deducted** with no transparency, which is a significant trust issue in a crypto product
---
 
## 📝 Note
 
This was a real QA assessment assigned by Sapher AllHeart Pvt Ltd. All testing was performed on the provided test environment using a test coin provided upon signup. No production data was affected.
