# FE-09: Testing Pass — Vitest, React Testing Library & Playwright E2E Suite

**Track:** Frontend AI Engineering  
**Week:** Week 6  
**Assignment Code:** FE-09  
**Author:** Aayush Kumar Singh  
**Live Application URL:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)  
**GitHub Repository:** [https://github.com/Aayush9-spec/frontend-ai-capstone](https://github.com/Aayush9-spec/frontend-ai-capstone)  

---

## 1. Executive Summary & Testing Philosophy

Tests are how AI-assisted developers build with confidence. An autonomous AI agent or subagent can write and refactor code safely only when a comprehensive automated test suite acts as an instant feedback loop and regression safety net.

This assignment establishes a **production-grade testing architecture** combining:
1. **Unit & Component Testing:** Vitest + React Testing Library (RTL).
2. **Accessible Querying:** Querying exclusively by ARIA roles, accessible labels, and text content (avoiding fragile `data-testid` reliance).
3. **API Layer Isolation:** Zero real network calls to live AI APIs in tests; all endpoints mocked via MSW (Mock Service Worker) / Vitest mocks.
4. **End-to-End Testing:** Playwright walking the primary user flow.
5. **Continuous Integration (CI):** GitHub Actions workflow blocking merges on test failures.

---

## 2. Test Suite Architecture & File Structure

```
__tests__/
├── components/
│   ├── ChatMessageRenderer.test.tsx  # Chat parts (text, code, tool invocation, error)
│   ├── ProjectInquiryForm.test.tsx   # Validated contact form with error states
│   └── ToolResultCard.test.tsx       # Structured tool result card & payload renderer
├── e2e/
│   └── primary_flow.spec.ts          # Playwright E2E full user journey
└── setup.ts                          # Vitest & RTL global configuration
```

---

## 3. High-Risk Component Test Coverage

### A. Component Test 1: Chat Message Renderer (`ChatMessageRenderer.test.tsx`)
Verifies that all message part types render correctly across lifecycle states:
- **Text Part:** Renders markdown paragraphs correctly.
- **Streaming State:** Displays animated cursor dot while `isStreaming=true`.
- **Tool Call Part:** Renders tool execution header and status badges.
- **Error State:** Renders error banner with retry trigger.
- **Accessible Query Example:** `screen.getByRole('article', { name: /assistant message/i })`

```tsx
import { render, screen } from '@testing-library/react';
import { ChatMessageRenderer } from '@/components/ChatMessageRenderer';

describe('ChatMessageRenderer', () => {
  it('renders streaming assistant message with accessible role', () => {
    render(
      <ChatMessageRenderer
        role="assistant"
        content="Generating code architecture..."
        isStreaming={true}
      />
    );
    expect(screen.getByRole('status')).toHaveTextContent(/generating code architecture/i);
    expect(screen.getByLabelText(/message streaming in progress/i)).toBeInTheDocument();
  });
});
```

### B. Component Test 2: Validated Inquiry Form (`ProjectInquiryForm.test.tsx`)
Verifies form validation rules and accessible error messages:
- Displays inline error when invalid email is entered (`screen.getByRole('alert')`).
- Disables submit button during active submission (`screen.getByRole('button', { name: /submitting/i })`).
- Displays success notification upon completion.

### C. Component Test 3: Tool Result Renderer (`ToolResultCard.test.tsx`)
Verifies structured tool execution outputs:
- Renders structured JSON payload into expandable code block.
- Confirms status indicator shows "Success" with accessible badge role.

---

## 4. End-to-End Playwright Suite (`primary_flow.spec.ts`)

```typescript
import { test, expect } from '@playwright/test';

test('Primary User Journey: Navigate, send AI chat message, and verify streaming response', async ({ page }) => {
  // 1. Visit home page
  await page.goto('/');

  // 2. Verify hero header is visible
  await expect(page.getByRole('heading', { level: 1 })).toBeVisible();

  // 3. Focus chat input and type prompt
  const chatInput = page.getByRole('textbox', { name: /ask AI assistant/i });
  await chatInput.fill('Explain Next.js App Router streaming');

  // 4. Click send button
  await page.getByRole('button', { name: /send message/i }).click();

  // 5. Verify assistant response streams and completes
  const responseMsg = page.getByRole('article').filter({ hasText: /App Router/i });
  await expect(responseMsg).toBeVisible({ timeout: 10000 });
});
```

---

## 5. Continuous Integration (CI) Workflow Setup

### GitHub Actions Workflow (`.github/workflows/ci.yml`)

```yaml
name: Continuous Integration

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'
      - name: Install dependencies
        run: npm ci
      - name: Run Vitest Unit & Component Suite
        run: npx vitest run --coverage
      - name: Install Playwright Browsers
        run: npx playwright install --with-deps
      - name: Run Playwright E2E Tests
        run: npx playwright test
```

---

## 6. Verification Results

```
 ✓ src/__tests__/components/ChatMessageRenderer.test.tsx (4 tests) 142ms
 ✓ src/__tests__/components/ProjectInquiryForm.test.tsx (3 tests) 98ms
 ✓ src/__tests__/components/ToolResultCard.test.tsx (2 tests) 65ms

 Test Files  3 passed (3)
      Tests  9 passed (9)
   Start at  15:58:12
   Duration  410ms (transform 85ms, setup 60ms, collect 110ms, tests 305ms)

 ✓ Playwright E2E Suite: 1 passed (12.4s)
```

- **All tests green in CI workflow.**
