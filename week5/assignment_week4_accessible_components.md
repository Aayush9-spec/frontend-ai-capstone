# Assignment: Accessible Component Fundamentals
**Student:** Aayush Kumar Singh  
**Track:** Front-end AI Engineering (Week 4)  
**ID:** `FE-03`  

---

## 1. Custom Hand-Built Components Implementation Summary (`playground/`)
Built three accessible interactive components from scratch in React + TypeScript without third-party component UI libraries:

### 1. Modal Dialog Component (`Modal.tsx`)
- **ARIA Attributes:** `role="dialog"`, `aria-modal="true"`, `aria-labelledby`, `aria-describedby`.
- **Focus Management:** Focus is automatically trapped within the modal when open using `onKeyDown` container trap logic. Restores focus back to the triggering element upon closure.
- **Keyboard Navigation:** `Escape` key closes the dialog. `Tab` and `Shift+Tab` cycle strictly between interactive modal elements.

### 2. Tabs Component (`Tabs.tsx`)
- **ARIA Attributes:** `role="tablist"`, `role="tab"`, `aria-selected="true|false"`, `role="tabpanel"`, `aria-controls`.
- **Keyboard Navigation:** `ArrowRight` and `ArrowLeft` keys cycle active tabs. `Home` jumps to first tab, `End` jumps to last tab.

### 3. Disclosure / Accordion Component (`Disclosure.tsx`)
- **ARIA Attributes:** `<button aria-expanded="true|false" aria-controls="panel-id">`, `<div id="panel-id" role="region">`.
- **Keyboard Navigation:** `Enter` or `Space` toggles open/closed states.

---

## 2. Comparative Analysis Notes (`NOTES.md`: Hand-Built vs. `shadcn/ui`)

### Key Gaps & Edge Cases Discovered in Custom Implementation:
1. **Focus Trap Edge Cases & Portal Rendering:**  
   Our hand-built modal managed focus via manual event handlers within a top-level div. `shadcn/ui` (via Radix UI Primitives) mounts dialogs into a React Portal (`document.body`) and uses `@radix-ui/react-focus-scope` to prevent background DOM interaction (`aria-hidden` on app root and scroll locking).
2. **Dynamic Screen Reader Announcements & Animations:**  
   `shadcn/ui` automatically handles CSS animation unmounting (`[data-state=open|closed]`) and manages screen-reader focus restoration even when the trigger element is dynamically unmounted from the DOM.
3. **Sub-component Composition Pattern:**  
   `shadcn` utilizes compound component architecture (`Dialog`, `DialogTrigger`, `DialogContent`, `DialogHeader`) maintaining clean prop interfaces and zero `any` TypeScript escapes.

---

## 3. Verification Self-Check
- [x] Three interactive components built from scratch in React + TypeScript.
- [x] Full keyboard operation verified (Tab, Escape, Arrow keys).
- [x] Focus trap & restoration implemented for modal.
- [x] `NOTES.md` documents 3 concrete gaps comparing custom code to `shadcn/ui`.
- [x] TypeScript compiles with 0 `any` escapes.
