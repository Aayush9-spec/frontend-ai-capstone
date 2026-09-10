# Assignment FE-07: Tool Results and Structured Output in the UI
**Student:** Aayush Kumar Singh  
**Track:** Front-end AI Engineering (Week 5)  
**ID:** `FE-07`  

---

## 1. Tool Definition Contract (`app/api/chat/tools.ts`)
```typescript
import { z } from 'zod';

export const leadScoringTool = {
  description: 'Evaluates and scores a lead based on project requirements, timeline, and tech stack match.',
  parameters: z.object({
    clientName: z.string().describe('Name of client or project lead'),
    budgetTier: z.enum(['starter', 'growth', 'enterprise']).describe('Budget allocation tier'),
    techStack: z.array(z.string()).describe('Technologies required for the project'),
    timelineWeeks: z.number().describe('Estimated project duration in weeks'),
  }),
  execute: async ({ clientName, budgetTier, techStack, timelineWeeks }) => {
    const baseScore = budgetTier === 'enterprise' ? 90 : budgetTier === 'growth' ? 75 : 60;
    const score = Math.min(100, baseScore + techStack.length * 2);
    
    return {
      clientName,
      score,
      recommendation: score >= 80 ? 'High Priority Lead' : 'Standard Lead',
      suggestedArchitecture: techStack.includes('Next.js') ? 'Vercel Edge Network' : 'Standard Node Container',
      timestamp: new Date().toISOString(),
    };
  },
};
```

---

## 2. Four Tool Part States Implementation (`components/ToolStateCard.tsx`)

| Tool Part State | Visual Treatment & User Question Answered | Component Render |
|---|---|---|
| **1. Input Streaming** | *What is the AI doing?* Display subtle animated pulse spinner with `[Calling Lead Scorer...]` badge. | Skeleton Card with pulsing border (`border-blue-500/50`) |
| **2. Input Available** | *With what parameters?* Display structured parameters pill tags (Budget, Tech Stack, Timeline). | Parameters Badge Grid |
| **3. Output Available** | *What came back?* Render full Lead Score Graphic Card with color-coded score badge and recommendations. | `LeadScoreCard.tsx` (Empirical Gauge + Details) |
| **4. Output Error** | *What went wrong?* Red warning banner with error reason, fallback message, and manual retry button. | `ToolErrorAlert.tsx` with `onRetry()` callback |

---

## 3. Structured UI Component Rendering (`components/LeadScoreCard.tsx`)
```tsx
export function LeadScoreCard({ result }: { result: any }) {
  return (
    <div className="p-4 my-2 border border-slate-700 rounded-xl bg-slate-900 text-slate-100 shadow-md">
      <div className="flex justify-between items-center mb-2">
        <h4 className="font-semibold text-sm">{result.clientName} Evaluation</h4>
        <span className={`px-2.5 py-0.5 rounded-full text-xs font-bold ${result.score >= 80 ? 'bg-emerald-950 text-emerald-400 border border-emerald-800' : 'bg-amber-950 text-amber-400 border border-amber-800'}`}>
          Score: {result.score} / 100
        </span>
      </div>
      <p className="text-xs text-slate-400">Recommendation: <strong className="text-slate-200">{result.recommendation}</strong></p>
      <p className="text-xs text-slate-400">Architecture: <span className="text-slate-200">{result.suggestedArchitecture}</span></p>
    </div>
  );
}
```

---

## 4. Deliverable Verification Links
* **Tool Definition Source:** https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/week5/fe07_tool_results.md
* **Live Interactive Demo URL:** https://frontend-ai-capstone.vercel.app/chat
