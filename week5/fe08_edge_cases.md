# Assignment FE-08: Error States, Empty States, Edge Cases
**Student:** Aayush Kumar Singh  
**Track:** Front-end AI Engineering (Week 5)  
**ID:** `FE-08`  

---

## 1. Inventory of Handled Edge Cases & Sabotage Testing Results

| Failure / Edge Case Scenario | Test Injection Method | Handled UX Treatment & Recovery Action |
|---|---|---|
| **1. Mid-Stream Network Drop** | Severed TCP connection during token chunk 15. | App displays `StreamInterruptedAlert` with custom red warning banner and active `[Retry Stream ↻]` button. |
| **2. API Rate Limit / 429 Error** | Returned 429 HTTP status from edge route handler. | App catches error in `onError` callback and renders `RateLimitBanner` explaining reset timing (60s countdown). |
| **3. Empty Search / Zero Results** | Submitted prompt query for non-existent case study. | Renders `EmptyStateContainer` with helpful suggestion pills (*"Try searching for React streaming or ARIA accessibility"*). |
| **4. First-Run Initial State** | Cleared local storage and opened fresh session. | Shows warm, clean welcome state with sample prompt starter buttons rather than a blank empty screen. |

---

## 2. Deliverable Verification Links
* **Error & Empty State Documentation:** https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/week5/fe08_edge_cases.md
* **Live Interactive Demo:** https://frontend-ai-capstone.vercel.app/chat
