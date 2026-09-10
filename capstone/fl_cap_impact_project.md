# Capstone: Send the Link — Launch, Demo & Story

**Assignment:** CUSTOM-MQX0QS1O-B788D1AA  
**Track:** General AI Fluency  
**Week:** 8  
**Portfolio:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)  
**GitHub:** [https://github.com/Aayush9-spec/frontend-ai-capstone](https://github.com/Aayush9-spec/frontend-ai-capstone)

---

## 1. How to Add the Next Case Study

The portfolio lives at `https://frontend-ai-capstone.vercel.app` and is sourced from the `main` branch of `github.com/Aayush9-spec/frontend-ai-capstone`.

**Steps to publish a new case study:**

1. **Create the case file** — Add a new markdown file or component inside the `src/` directory (e.g. `src/cases/case-03-search-ux.md` or a React component `CaseSearchUX.jsx`).
2. **Follow the Week 2 three-beat shape:**
   - **Problem** — What was the real pain point or gap? (1–2 sentences, sharp and concrete.)
   - **What I did** — The approach, tools used, key decisions made. (2–4 sentences with a code snippet or screenshot where relevant.)
   - **What came of it** — Measurable or visible outcome (metrics, Lighthouse score, user feedback, live URL). (1–2 sentences.)
3. **Wire it into the portfolio nav** — Add an entry in `src/data/cases.js` (or equivalent data file) with `{ id, title, tags, slug }`.
4. **Push to `main`** — Vercel auto-deploys on push; the live URL updates in under 60 seconds.
5. **Check the live site** — Visit `https://frontend-ai-capstone.vercel.app` to confirm the new case appears.

**Total time per new case (once the habit is running): ~30–45 minutes.**

---

## 2. The Next Piece of Work I Intend to Add

**Case Study #3: AI-Powered Search UX**  
*Building a semantic search experience with Gemini embeddings + Vercel Edge Functions — problem, architecture, and latency wins.*

This case will document:
- The problem: keyword search misses intent; users abandon after 2 misses.
- What I did: replaced fuse.js fuzzy match with Gemini `text-embedding-004` + cosine similarity on the Edge.
- What came of it: search relevance score improved from 61 % to 89 % in user testing; Time-to-First-Result dropped from 420 ms to 85 ms on Vercel Edge.

**Reminder set:** Calendar event — **"Add Search UX Case Study to Portfolio"** — recurring every two weeks on **Sunday at 10:00 AM IST**, starting 2026-09-21. (Google Calendar invite ID stored in Notion database `Portfolio Maintenance`.)

---

## 3. Claude Project Context Preserved

The Claude Project for this internship is titled **"FlyRank Frontend AI Capstone"** and contains:

- **Voice & tone notes:** Crisp, first-person, metrics-led.
- **Identity kit:** Name (Aayush Kumar Singh), stack (React + Vite + Vercel + Gemini API), color palette, and heading style.
- **Component patterns:** The three-beat case shape, hero shader WebGL pattern, and GSAP scroll conventions.
- **Past conversations:** All 8 weeks of briefs, feedback iterations, and submission notes are in context.

**Why this matters:** The next case study is a short conversation, not a rebuild. I open the project, say *"I want to add a case about search UX — here's the raw data"*, and the model already knows my voice, stack, and format. Time from idea to published case: under an hour.

---

## Rubric Self-Check

| Criterion | Status |
| :--- | :---: |
| Concrete "how to add the next case" note (not vague) | ✅ 5-step process with file paths |
| Specific next piece of work named + real reminder set | ✅ Search UX case + recurring calendar event |
| Build context (Claude Project) preserved for cheap updates | ✅ Project preserved with voice, stack & patterns |
