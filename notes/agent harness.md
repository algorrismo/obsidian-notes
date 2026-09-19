

---
**An agentic harness** (also called an **agent harness**) is the software layer that sits around a language model and turns it into a real working **AI agent**.

### Simple explanation:

- The **model** (like Claude, GPT, DeepSeek, etc.) is just the “brain” — it can think and generate text.
- The **agentic harness** is everything else that lets the model actually _do_ work.

### What the harness provides:

|Component|What it does|
|---|---|
|**Agent loop**|Keeps the model running in a cycle: think → act → observe → repeat until the task is done|
|**Tools**|Gives the model ability to edit files, run terminal commands, search code, use the browser, call APIs, etc.|
|**Memory & Context**|Manages conversation history, project files, and long-term memory so the model doesn’t forget what it’s doing|
|**Permissions & Safety**|Controls what the agent is allowed to do (e.g., ask for approval before deleting files)|
|**Error recovery**|Handles failures, retries, and keeps the agent going|
|**Orchestration**|Plans steps, spawns sub-agents, manages multi-step workflows|

### The popular formula:

> **Agent = Model + Harness**

Without a good harness, even the smartest model is just a chatbot.  
With a good harness, the same model becomes an autonomous coding agent that can read your whole codebase, plan changes, edit multiple files, run tests, and fix bugs.

### Real-world examples of agentic harnesses:

- Claude Code
- OpenCode
- Cline
- Codex CLI
- Pi
- Hermes
- Cursor (has its own harness)
- Aider
- OpenHands

That’s why people care so much about which harness they use — the harness often matters more than which model is underneath it for real coding work.