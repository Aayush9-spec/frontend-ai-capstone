# Assignment: Three Roads - Choose Your Stack with AI
**Student:** Aayush Kumar Singh  
**Track:** General AI Fluency (Week 4)  
**ID:** `CUSTOM-MQX06U8B-9AAA4FBA`  

---

## 1. Input Constraints Provided to AI
1. **Hosting & Licensing Constraint:** 100% Free tier only (no required credit card or surprise charges).
2. **Skill Level:** Proficient in React, TypeScript, Next.js, and modern web APIs; comfortable with git & deployment pipelines.
3. **Portfolio Purpose (From Sitemap & Content Map):** Showcase live interactive React AI components, high-density case studies, empirical benchmark charts, and code repositories.
4. **Display & Media Needs:** Fast initial page loads (<1.2s), embedded live interactive widgets, code syntax highlighting, clean responsive layout across mobile and desktop.

---

## 2. Evaluation of Three Stack Options

### Option A: Static Site Generator (Astro + Vanilla HTML/CSS + Markdown)
- **Build Approach:** Content-focused SSG rendering static HTML with zero JavaScript by default; island architecture for interactive widgets.
- **Free Hosting Provider:** Cloudflare Pages / GitHub Pages.
- **Backend Requirement:** None (Static).
- **Key Trade-off:** Exceptional performance and zero hosting cost, but adds complexity when embedding dynamic client-side React state or interactive AI API callers.

### Option B: Full-Stack React Framework (Next.js App Router + TypeScript + Tailwind CSS) [CHOSEN STACK]
- **Build Approach:** React-based single-page / server-rendered application with component-driven architecture.
- **Free Hosting Provider:** Vercel (Hobby Tier).
- **Backend Requirement:** Optional serverless API routes (`/api/chat` or `/api/eval`), currently set to static / client-side API execution.
- **Key Trade-off:** Slightly heavier JS bundle than pure static HTML, but provides maximum flexibility for live React component demos, dynamic UI state, and seamless deployment on Vercel.

### Option C: No-Code Portfolio Builder (Framer / Webflow)
- **Build Approach:** Visual drag-and-drop builder with pre-made templates.
- **Free Hosting Provider:** Framer free subdomain (`.framer.media`).
- **Backend Requirement:** None.
- **Key Trade-off:** Extremely fast visual setup, but zero ability to showcase raw React/TypeScript source code, custom ARIA accessibility patterns, or custom interactive client-side logic.

---

## 3. Pressure-Test & Rationale for Chosen Stack (Next.js + TypeScript + Vercel)
- **Feasibility & Speed:** Next.js with TypeScript allows direct reuse of components built in `FE-01`, `FE-03`, and `FE-04` drills without code translation.
- **Display Accuracy:** Supports high-fidelity syntax highlighting, interactive component sandboxes, and custom ARIA keyboard navigation.
- **Maintenance Burden:** Continuous deployment via Git pushes to Vercel requires zero server configuration or infrastructure maintenance.
- **Conclusion:** Option B best balances technical proof display with zero-cost hosting and long-term maintainability.

---

## 4. Verification Self-Check
- [x] 3 distinct options evaluated with trade-offs.
- [x] Tailored to 100% free tier and project display requirements.
- [x] Rationale written in student's own words.
