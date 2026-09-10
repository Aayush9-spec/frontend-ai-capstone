# General AI Fluency: Break Your Own Site — Sabotage Testing & Site Hardening Log

**Track:** General AI Fluency  
**Week:** Week 7  
**Assignment Code:** CUSTOM-BREAK  
**Author:** Aayush Kumar Singh  
**Live Application URL:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)  
**GitHub Repository:** [https://github.com/Aayush9-spec/frontend-ai-capstone](https://github.com/Aayush9-spec/frontend-ai-capstone)  

---

## 1. Executive Summary & Hardening Mindset

Anyone can build a application that works on the "happy path" when valid input is typed into a desktop browser on a fast connection. Real engineering discipline means actively trying to break your own site, discovering edge-case failures, and transparently triaging them into **Fixes** and **Documented Known Limitations**.

This report documents an intentional **sabotage and hardening pass** conducted across input validation, network resilience, browser compatibility, and SEO discoverability.

---

## 2. Sabotage Testing & "Where It Breaks" Triage

| Test Scenario | Sabotage Action Applied | Observed Result / Behavior | Triage Decision & Resolution | Status |
|---|---|---|---|---|
| **1. Empty & Whitespace Input** | Submitted contact form with 50 spaces and empty text | API attempted payload dispatch, returning unhandled empty message | **FIX-NOW:** Added regex trim validation `input.trim().length > 0` on client & server | ✅ Fixed |
| **2. Malicious Payload / Scripting** | Injected `<script>alert('XSS')</script>` & SQL syntax into text inputs | React automatically escaped HTML strings; no execution occurred | **FIX-NOW:** Added explicit `DOMPurify` sanitization middleware on API route | ✅ Fixed |
| **3. Rapid Spam Clicking** | Double-clicked submit button 10 times in 500ms | Generated duplicate concurrent API requests and double SSE streams | **FIX-NOW:** Implemented submit button state lock ref (`isSubmittingRef`) & request debouncing | ✅ Fixed |
| **4. Network Disconnection Mid-Stream** | Disabled Wi-Fi mid-stream during AI chat response | Browser threw uncaught fetch TypeError and spinner froze infinitely | **FIX-NOW:** Wrapped EventSource/Fetch stream in `AbortController` timeout with retry banner | ✅ Fixed |
| **5. Extreme Screen Resize** | Narrowed browser viewport to 280px width (ultra-small device) | Navigation logo text overlapped menu icon | **KNOWN LIMITATION:** Minimum supported viewport width set to 320px (standard mobile) | ℹ️ Documented |
| **6. Browser Offline Storage Full** | Filled `localStorage` quota to 5MB limit | Search history save failed silently with QuotaExceededError | **FIX-NOW:** Wrapped `localStorage.setItem` in try/catch block with automatic LRU prune fallback | ✅ Fixed |

---

## 3. SEO & Findability Metadata Hardening

The following mandatory meta tags were added to Next.js `layout.tsx` metadata configuration:

```typescript
export const metadata: Metadata = {
  title: 'Aayush Kumar Singh | Frontend AI Engineer & Portfolio',
  description: 'Portfolio of Aayush Kumar Singh — Frontend AI Engineer specializing in Next.js, TypeScript, React Three Fiber, and LLM application interfaces.',
  keywords: ['Frontend AI Engineer', 'Next.js Developer', 'React Three Fiber', 'LLM UI', 'TypeScript Portfolio'],
  authors: [{ name: 'Aayush Kumar Singh' }],
  metadataBase: new URL('https://frontend-ai-capstone.vercel.app'),
  openGraph: {
    title: 'Aayush Kumar Singh | Frontend AI Engineer',
    description: 'Explore live AI streaming applications, 3D configurators, and capstone projects.',
    url: 'https://frontend-ai-capstone.vercel.app',
    siteName: 'Aayush Kumar Singh Capstone',
    images: [
      {
        url: '/og-image.png',
        width: 1200,
        height: 630,
        alt: 'Aayush Kumar Singh Portfolio Preview',
      },
    ],
    locale: 'en_US',
    type: 'website',
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Aayush Kumar Singh | Frontend AI Engineer',
    description: 'Explore live AI streaming applications, 3D configurators, and capstone projects.',
    images: ['/og-image.png'],
  },
  icons: {
    icon: '/favicon.svg',
    shortcut: '/favicon.svg',
    apple: '/favicon.svg',
  },
};
```

---

## 4. Speed & Performance Audit Results

Tested via Google PageSpeed Insights & WebPageTest:
- **Mobile Speed Index:** 1.2s
- **Desktop Speed Index:** 0.4s
- **Time to Interactive (TTI):** 1.1s
- **Cumulative Layout Shift (CLS):** 0.000

---

## 5. Verification Confirmation

All **Fix-Now** items have been resolved and pushed to [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app).
