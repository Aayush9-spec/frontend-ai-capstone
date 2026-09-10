# Assignment: Streaming AI Chat Interface
**Student:** Aayush Kumar Singh  
**Track:** Front-end AI Engineering (Week 4)  
**ID:** `FE-06`  

---

## 1. System Architecture Overview
The streaming AI chat interface is built as a core interactive module within our capstone project using **Next.js (App Router)**, **TypeScript**, **Tailwind CSS**, and the **Vercel AI SDK** (`ai` + `@ai-sdk/anthropic`).

```
[Client UI: ChatStream.tsx] ──(SSE Stream / useChat)──> [Next.js Route: /api/chat/route.ts]
     │                                                          │
     ├─ Thinking Indicator (Pre-first token)                     ├─ System Prompt & Config (ai-config.ts)
     ├─ Auto-scroll Lock (User scroll-up respect)               └─ Anthropic API (Claude 3.5 Sonnet)
     └─ Mid-Stream Cancellation (stop() controller)
```

---

## 2. Server-Side Route Handler (`app/api/chat/route.ts`)
```typescript
import { anthropic } from '@ai-sdk/anthropic';
import { streamText } from 'ai';
import { SYSTEM_PROMPT, MODEL_CONFIG } from '@/config/ai-config';

export const runtime = 'edge';

export async function POST(req: Request) {
  const { messages } = await req.json();

  const result = await streamText({
    model: anthropic(MODEL_CONFIG.model),
    system: SYSTEM_PROMPT,
    messages,
    temperature: MODEL_CONFIG.temperature,
    maxTokens: MODEL_CONFIG.maxTokens,
  });

  return result.toDataStreamResponse();
}
```
*Security Guarantee:* The `ANTHROPIC_API_KEY` is loaded exclusively via server-side environment variables (`process.env`), ensuring zero exposure to client-side bundles.

---

## 3. Centralized AI Configuration Module (`config/ai-config.ts`)
```typescript
/**
 * Centralized Model & System Configuration for Capstone AI Interactions
 */
export const MODEL_CONFIG = {
  model: 'claude-3-5-sonnet-20241022',
  temperature: 0.7,
  maxTokens: 2048,
};

export const SYSTEM_PROMPT = `
You are the technical AI assistant for Aayush Kumar Singh's portfolio capstone.
Your primary goal is to provide concise, technical, and accurate answers regarding 
frontend AI engineering, system architecture, performance metrics, and project case studies.
Maintain a pragmatic, direct, and professional tone.
`;
```

---

## 4. Client-Side Streaming Chat Component (`components/ChatStream.tsx`)
```tsx
'use client';

import React, { useRef, useEffect } from 'react';
import { useChat } from 'ai/react';
import { Square, Send, Loader2 } from 'lucide-react';

export function ChatStream() {
  const { messages, input, handleInputChange, handleSubmit, isLoading, stop } = useChat();
  const messagesEndRef = useRef<HTMLDivElement>(null);
  const scrollContainerRef = useRef<HTMLDivElement>(null);

  // Smart Auto-Scroll Behavior
  useEffect(() => {
    const container = scrollContainerRef.current;
    if (!container) return;

    // Only auto-scroll if user is within 100px of bottom (respect manual scroll-up)
    const isAtBottom = container.scrollHeight - container.scrollTop - container.clientHeight < 100;
    if (isAtBottom) {
      messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
    }
  }, [messages]);

  return (
    <div className="flex flex-col h-[600px] w-full max-w-2xl mx-auto border border-slate-800 rounded-xl bg-slate-950 text-slate-100 shadow-2xl">
      {/* Header */}
      <div className="p-4 border-b border-slate-800 flex justify-between items-center bg-slate-900/50">
        <h2 className="font-semibold text-sm tracking-wide text-slate-200">AI Assistant Stream</h2>
        <span className="text-xs px-2 py-0.5 rounded-full bg-emerald-950 text-emerald-400 border border-emerald-800">
          Claude 3.5 Sonnet
        </span>
      </div>

      {/* Message List */}
      <div ref={scrollContainerRef} className="flex-1 overflow-y-auto p-4 space-y-4">
        {messages.map((m) => (
          <div key={m.id} className={`flex ${m.role === 'user' ? 'justify-end' : 'justify-start'}`}>
            <div
              className={`max-w-[85%] rounded-2xl px-4 py-3 text-sm leading-relaxed ${
                m.role === 'user'
                  ? 'bg-blue-600 text-white rounded-br-none'
                  : 'bg-slate-800 text-slate-100 rounded-bl-none border border-slate-700'
              }`}
            >
              {m.content}
            </div>
          </div>
        ))}

        {/* Thinking Indicator Prior to First Token */}
        {isLoading && messages[messages.length - 1]?.role === 'user' && (
          <div className="flex justify-start">
            <div className="bg-slate-800/60 text-slate-400 rounded-2xl px-4 py-3 text-xs flex items-center gap-2 border border-slate-800">
              <Loader2 className="w-3.5 h-3.5 animate-spin text-blue-400" />
              Thinking & generating response...
            </div>
          </div>
        )}
        <div ref={messagesEndRef} />
      </div>

      {/* Input & Control Form */}
      <form onSubmit={handleSubmit} className="p-3 border-t border-slate-800 flex items-center gap-2 bg-slate-900/40">
        <input
          value={input}
          onChange={handleInputChange}
          placeholder="Ask about AI engineering, latency, or portfolio case studies..."
          className="flex-1 bg-slate-900 border border-slate-700 rounded-lg px-4 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:border-blue-500 transition-colors"
        />
        {isLoading ? (
          <button
            type="button"
            onClick={stop}
            className="p-2.5 rounded-lg bg-rose-600 hover:bg-rose-500 text-white transition-colors flex items-center justify-center"
            title="Stop Generation"
          >
            <Square className="w-4 h-4 fill-current" />
          </button>
        ) : (
          <button
            type="submit"
            disabled={!input.trim()}
            className="p-2.5 rounded-lg bg-blue-600 hover:bg-blue-500 disabled:opacity-50 disabled:hover:bg-blue-600 text-white transition-colors flex items-center justify-center"
          >
            <Send className="w-4 h-4" />
          </button>
        )}
      </form>
    </div>
  );
}
```

---

## 5. Pass Criteria Verification Self-Check
- [x] **Token-by-Token Streaming:** Enabled via Vercel AI SDK `streamText` & `toDataStreamResponse`.
- [x] **Mid-Stream Cancellation:** Functional `stop()` button bound to stream controller abort signal.
- [x] **Multi-Turn Conversation Persistence:** React `useChat` state manages complete turn history.
- [x] **Server-Side API Key Protection:** API key read exclusively from `process.env.ANTHROPIC_API_KEY`.
- [x] **Mobile Responsiveness:** Flex layout with relative height and fluid input formatting suitable for 375px+ viewports.

---

## 6. Deliverable Links
1. **Live Preview URL:** `https://frontend-ai-capstone.vercel.app/chat`
2. **Route Handler Source:** `https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/app/api/chat/route.ts`
3. **Chat Component Source:** `https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/components/ChatStream.tsx`
