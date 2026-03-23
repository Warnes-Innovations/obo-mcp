---
description: "Process multiple items sequentially with priority scoring, resume handling, and persistent OBO session state"
name: "OBO Review Session"
argument-hint: "Optional context or item source such as a finding list, task list, or requirements"
agent: "agent"
tools: [obo-mcp/*]
---

Use the `obo-mcp` MCP server to manage a One-By-One review session for the current workspace.

Follow this workflow:

1. Call `obo_list_sessions` for the current workspace before extracting new items.
2. If an incomplete session exists, ask whether to resume, merge, defer, replace, or stop.
3. If creating a new session, extract discrete items from the current context.
4. Assign priority factors for each item using urgency, importance, effort, and dependencies.
5. Call `obo_create` to persist the session.
6. If adding to an existing session, call `obo_merge_items`.
7. Present an executive summary before reviewing individual items.
8. Use `obo_next` to choose the next actionable item.
9. Use `obo_mark_in_progress` when work begins on an item.
10. After user approval or denial, use `obo_mark_complete` or `obo_mark_skip`.
11. Use `obo_session_status` to report progress after each decision.
12. When no actionable items remain, call `obo_complete_session`.

Rules:

- Never directly edit `.github/obo_sessions/*.json` or `index.json`.
- Never synthesize session state from manual file writes when an `obo_*` tool exists.
- Prefer OBO for multi-item workflows that need resumable queue state; prefer normal chat for one-off tasks.
- Present one item at a time and do not advance until the user explicitly approves, denies, skips, or asks to move on.
- If the MCP surface cannot perform a requested operation, stop and tell the user what is missing.

Input to process: ${input}
