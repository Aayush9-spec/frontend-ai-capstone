# General AI Fluency: Make It Do Something — End-to-End Live Feature

**Track:** General AI Fluency  
**Week:** Week 6  
**Assignment Code:** CUSTOM-MAKE-IT  
**Author:** Aayush Kumar Singh  
**Live Application URL:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)  
**GitHub Repository:** [https://github.com/Aayush9-spec/frontend-ai-capstone](https://github.com/Aayush9-spec/frontend-ai-capstone)  

---

## 1. Feature Overview & Selection

A static portfolio shows what you can design, but a **functional portfolio feature** proves you know how software actually works end-to-end. 

For this assignment, I implemented an **AI-Powered Interactive Contact & Project Inquiry System**. Visitors can submit project inquiries or message prompts directly on the live portfolio site. The system processes inputs, runs server-side validation, invokes the AI backend stream, and securely stores/routes the message.

---

## 2. Plain-English Explainer: How Software & Backends Work

### What is a Backend?
Think of a website like a restaurant:
- The **Frontend (UI)** is the dining area and the physical menu. It's what the customer sees, clicks, and interacts with.
- The **Backend (Server)** is the kitchen behind closed doors. Customers aren't allowed in the kitchen for safety, privacy, and hygiene reasons. The backend handles sensitive logic: storing confidential data, checking passwords, processing payments, and communicating with external AI models.

### What Does This Feature Do?
When a visitor fills out the contact form or submits a chat prompt:
1. The user types their email and message in their web browser.
2. The web browser sends an HTTP POST request containing JSON data over the internet to our Vercel Serverless Backend.
3. The Vercel Backend validates the input, ensures rate limits aren't exceeded, calls the Google Gemini AI API using an encrypted secret key, and streams back the structured response.
4. The frontend updates dynamically on screen without reloading the page.

---

## 3. End-to-End Data Flow Architecture

```
┌────────────────────────┐              ┌────────────────────────┐              ┌────────────────────────┐
│   User Browser (UI)    │              │ Vercel Serverless API  │              │ Google Gemini AI API   │
│ (React + Next.js App)  │              │  (Next.js App Router)  │              │  (Secure Remote LLM)   │
└───────────┬────────────┘              └───────────┬────────────┘              └───────────┬────────────┘
            │                                       │                                       │
            │  1. Submit Form Data (POST /api/chat)  │                                       │
            ├──────────────────────────────────────►│                                       │
            │                                       │  2. Sanitize & Verify Rate Limit      │
            │                                       ├──────────────────┐                    │
            │                                       │                  │                    │
            │                                       │◄─────────────────┘                    │
            │                                       │                                       │
            │                                       │  3. Formulate Prompt & Send Key       │
            │                                       ├──────────────────────────────────────►│
            │                                       │                                       │
            │                                       │  4. Stream Token Chunks               │
            │                                       │◄──────────────────────────────────────┤
            │  5. Server-Sent Events (SSE) Stream   │                                       │
            │◄──────────────────────────────────────┤                                       │
            │                                       │                                       │
            │  6. Render Dynamic UI Response        │                                       │
            ├──────────────────┐                    │                                       │
            │                  │                    │                                       │
            │◄─────────────────┘                    │                                       │
```

---

## 4. Free-Tier Infrastructure Setup

- **Hosting:** Vercel Hobby Free Tier (Serverless Functions with 10s execution limits).
- **Frontend Framework:** Next.js 14 App Router + Tailwind CSS.
- **Backend API:** Next.js Route Handlers (`app/api/chat/route.ts`).
- **Database / Key Storage:** Vercel Environment Variables (`GEMINI_API_KEY`) for secure key protection.

---

## 5. Verification & Live Evidence

- **Test Submission:** Verified live test submissions reached the backend and generated real AI responses.
- **Live URL:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)
