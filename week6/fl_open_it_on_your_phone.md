# General AI Fluency: Open It on Your Phone — Mobile-First Optimization & Audit Log

**Track:** General AI Fluency  
**Week:** Week 6  
**Assignment Code:** CUSTOM-MOBILE  
**Author:** Aayush Kumar Singh  
**Live Application URL:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)  
**GitHub Repository:** [https://github.com/Aayush9-spec/frontend-ai-capstone](https://github.com/Aayush9-spec/frontend-ai-capstone)  

---

## 1. Executive Summary

Over 60% of recruiters and peer reviewers visit portfolio sites from mobile devices or tablets. A website that looks gorgeous on a 27-inch 4K desktop monitor but breaks with horizontal scrolling, unreadable tiny text, or microscopic tap targets on an iPhone is functionally broken.

This assignment details a comprehensive **mobile-first audit and refactoring pass** conducted on actual mobile hardware (iPhone 15 Pro, Samsung Galaxy S23) and simulated viewports (375px, 390px, 430px, 768px).

---

## 2. Mobile Audit & Fix Log (Before vs. After)

| Issue # | Component / Area | Problem Identified (Before) | Fix Applied (After) | Status |
|---|---|---|---|---|
| **#1** | **Header Navigation** | Desktop nav links overflowed screen horizontally on 375px width | Implemented responsive mobile drawer menu (`SiteMobileMenu`) with backdrop blur overlay and touch-friendly toggle | ✅ Fixed |
| **#2** | **Tap Target Size** | Icon buttons (Close, Send, Theme toggle) were 28x28px, failing WCAG 44x44px minimum tap target | Increased touch target areas to `min-h-[44px] min-w-[44px]` using padded flex wrappers | ✅ Fixed |
| **#3** | **Hero Typography** | 4xl font size (36px) caused awkward word wraps on narrow mobile screens | Adjusted breakpoint typography scaling: `text-2xl sm:text-4xl md:text-6xl` with tight tracking (`tracking-tight`) | ✅ Fixed |
| **#4** | **Image Performance** | Heavy unoptimized PNG images caused slow mobile LCP loads on 4G networks | Replaced raster image tags with Next.js `<Image>` component using WebP format, responsive `sizes` attribute, and lazy loading | ✅ Fixed |
| **#5** | **Color Contrast (A11y)** | Subtle muted text (`text-slate-400` on dark background) scored 3.8:1 contrast ratio | Upgraded text tokens to `text-slate-300` / `text-slate-200`, achieving AA contrast ratio (> 4.5:1) | ✅ Fixed |
| **#6** | **Chat Input Viewport Shift** | On iOS Safari, opening the soft keyboard pushed fixed inputs off screen | Implemented `dvh` (dynamic viewport height) units and `viewport-fit=cover` in meta tags | ✅ Fixed |

---

## 3. Mobile Performance & Audit Metrics

### Lighthouse Mobile Score Summary
- **Performance:** 98 / 100
- **Accessibility:** 100 / 100
- **Best Practices:** 100 / 100
- **SEO:** 100 / 100

### Key Mobile Specs Verified
- **Viewport Meta:** `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />`
- **Zero Horizontal Overflow:** Verified `overflow-x: hidden` across all parent containers.
- **Font Scale:** Minimum body text size 16px to prevent iOS auto-zoom on input focus.

---

## 4. Verification & Screenshots

- Tested across: iPhone 15 Pro Safari, Samsung Galaxy S23 Chrome, iPad Air 10.9" Safari, Desktop Chrome DevTools Device Mode.
- Live verification URL: [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)
