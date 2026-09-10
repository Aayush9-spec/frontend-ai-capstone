# Assignment: Explain It Like You Built It
**Student:** Aayush Kumar Singh  
**Track:** General AI Fluency (Week 5)  
**ID:** `CUSTOM-MQX0CE9V-B5BB265F`  

---

## 1. The Build Piece Chosen: How Next.js Serverless Edge Streaming Works
**Topic:** How Token Streaming Works from Anthropic Claude API → Next.js Edge Server → React Browser UI (`useChat`).

---

## 2. Plain-Words Explanation (Teaching a Friend)

Imagine you're at a restaurant ordering a custom 10-course meal, but instead of waiting 45 minutes for the chef to cook everything and bring out 10 plates all at once on a big tray, the waiter brings out each dish the exact second it finishes sizzling. 

That's the fundamental difference between **traditional REST API requests** and **Streaming WebSockets/Server-Sent Events (SSE)**.

1. **The Old Way (Non-streaming):** When you send a message to ChatGPT or Claude, your browser sends a request across the internet to the server. The server asks the AI model to generate the whole essay. The model sits there calculating for 8 seconds, generates 500 words, packages them into one giant JSON response, and sends it back. For 8 seconds, your screen looks completely frozen.
2. **The Streaming Way (What We Built):** 
   - When you click "Send" in our web app, your browser opens an HTTP POST connection to our server endpoint `/api/chat`.
   - Our Next.js server immediately connects to Anthropic's Claude API using an **Edge Runtime Stream**.
   - As Claude's neural network generates word pieces (called "tokens") every 30 milliseconds, Anthropic streams tiny data packets back to our Next.js server.
   - Our server doesn't hold onto them — it immediately forwards those chunks directly down to your browser over a single open HTTP connection called a **Server-Sent Event (SSE)** stream.
   - In the browser, our React component uses the `useChat` hook, which listens to that incoming text stream, appends each new letter to the screen instantly, and smooth-scrolls down.

---

## 3. Why Owning This Concept Matters
Understanding this flow allows us to handle real edge cases:
- If a user loses Wi-Fi mid-sentence, we know the SSE stream connection dropped, so we can display a clean red retry button instead of crashing the page.
- If the AI model takes 200ms before sending its first word, we display a "Thinking..." spinner so the user knows the server is actively working.

---

## 4. Deliverable Verification Links
* **Full Explanation Document:** https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/week5/explain_it_like_you_built_it.md
