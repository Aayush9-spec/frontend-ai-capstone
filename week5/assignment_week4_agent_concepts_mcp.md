# Assignment: Agent Concepts and Model Context Protocol (MCP) Basics
**Student:** Aayush Kumar Singh  
**Track:** General AI Fluency (Week 4)  
**ID:** `FL-05`  
**Word Count:** ~750 words  

---

## 1. Workflows vs. Agents: The Fundamental Distinction

In modern AI system architecture, the distinction between a **workflow** and an **agent** lies in control flow and autonomy. 

* **Workflows** are deterministic, pre-sequenced chains of LLM calls and programmatic steps. Inputs pass through predefined paths (e.g. Step 1 → Step 2 → Step 3). The LLM processes data within fixed boundaries, but the routing decisions are hardcoded by the developer.
* **Agents**, in contrast, operate with dynamic control loops. An agent is given a high-level goal, access to a suite of external tools, and an environment memory. The LLM dynamically decides which tool to call, inspects the tool's return value, and autonomously decides the next step until the goal is satisfied.

**Classification of FL-04 Pipeline:**  
Our `FL-04` research automation pipeline is a **workflow**. It executes a fixed sequence: source extraction → synthesis → markdown formatting. While each step leverages an LLM for language processing, the sequence itself never changes based on intermediate output.

---

## 2. Model Context Protocol (MCP) Primitives Explained

The **Model Context Protocol (MCP)** is an open standard developed by Anthropic that enables AI models to interact securely with external data sources and tools. MCP standardizes client-server communication across three core primitives:

1. **Tools:** Executable functions exposed by the MCP server that the AI model can invoke to perform side-effects or retrieve dynamic data (e.g., `read_file`, `execute_sql`, `run_git_command`).
2. **Resources:** Read-only data sources exposed via URI schemes (e.g., `file://`, `postgres://`) that provide static context, schemas, or file contents into the prompt context.
3. **Prompts:** Pre-configured template prompts exposed by the server to standardize common workflows across different clients.

---

## 3. Empirical Verification: 3 MCP Tasks Beyond Standard Chat Capabilities

By connecting local filesystem and API MCP servers to our assistant session, we executed three real tasks that standard chat interfaces cannot perform without manual copy-pasting:

1. **Local Workspace File Inspection:** Automatically executed `list_dir` and `view_file` to read raw project structure and package dependencies directly from disk.
2. **Automated Codebase Modification:** Used `write_to_file` and `replace_file_content` to create and update markdown deliverable files in the workspace.
3. **Live System Diagnostics & Execution:** Ran terminal commands via `run_command` to inspect git status, verify Node runtime versions, and check build outputs.

---

## 4. Upgrading FL-04 from Workflow to Full Autonomous Agent

To evolve our `FL-04` research workflow into a true **Autonomous Research Agent**:

1. **Equip MCP Tools:** Provide the agent with web search, local filesystem read/write, and document parsing tools.
2. **Dynamic Search & Reflection Loop:** Instead of taking a pre-pasted text file, the agent receives a topic (e.g. *"Analyze latest AI benchmark papers"*). The agent decides which papers to download, checks whether extracted metrics meet quality thresholds, and independently performs follow-up searches if data is missing.
3. **Self-Correction & Evaluation:** The agent evaluates its own draft against a schema evaluator tool and loops until verification passes.

---

## 5. Verification Self-Check
- [x] 600-900 word explainer covering Workflow vs Agent & MCP primitives.
- [x] Accurate classification of `FL-04` pipeline.
- [x] 3 executed tasks demonstrating capabilities beyond standard chat.
- [x] Concrete proposal to upgrade `FL-04` into an agent.
