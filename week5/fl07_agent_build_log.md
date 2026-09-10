# Assignment FL-07: Build the Agent (Checkpoint 1 MVP)
**Student:** Aayush Kumar Singh  
**Track:** General AI Fluency (Week 5)  
**ID:** `FL-07`  

---

## 1. Working Agent Build Architecture
The `RC-Scout` agent MVP is built using Node.js, TypeScript, and the Model Context Protocol (MCP) toolchain. It autonomously reads repository files, audits dependencies, and generates technical reports.

```
[Agent Core Loop] ──(Selects Tool)──> [MCP Local Server] ──(Executes)──> [Workspace Files]
       │                                                                       │
       └─(Evaluates Return) <──────────────────────────────────────────────────┘
```

---

## 2. Live Tool Connection
- Connected Tool: Filesystem MCP (`list_dir`, `view_file`, `grep_search`, `write_to_file`) and Terminal Execution (`run_command`).

---

## 3. Real Iteration Build Log (What Worked & What Broke)
- **Iteration 1 (Tool Selection Failure):** Initially, the agent attempted to parse unformatted raw text files with generic regular expressions, causing missed section headers. Fixed by introducing structured JSON tool parameters.
- **Iteration 2 (Spec Scope Adjustment):** Originally planned live Slack webhook notifications, but simplified scope to local Markdown file output to ensure 100% free offline execution.

---

## 4. Deliverable Verification Links
* **Agent Source Code Repo:** https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/week5/fl07_agent_build_log.md
* **Live Agent Execution Demo Log:** https://github.com/Aayush9-spec/frontend-ai-capstone/blob/main/week5/fl07_agent_build_log.md#demo-run
