# LinkedIn Post Draft

We built a small MCP server for a problem that comes up constantly with coding agents: handling multi-item work without losing track of what was already reviewed, approved, skipped, or deferred.

The approach is called One-by-One review sessions.

Instead of relying on a long chat transcript, the agent stores a real session with prioritized items, explicit status, and resumable state. That makes it much easier to review findings one at a time, pause, come back later, or hand the work to another session without reconstructing context from memory.

Why it matters:

- better than a flat wall of findings in chat
- more durable than a single turn of question buttons
- easier to resume after model restarts or editor reloads
- clearer approval flow for code review, planning, and issue triage

We packaged it as `obo-mcp`, with templates for Copilot, Codex, Claude Code, and Cline so teams can adopt the workflow instead of just the tool surface.

If you are working on agent UX, code review workflows, or MCP-based developer tooling, this pattern is worth a look.

Hashtags: #MCP #AIAgents #DeveloperTools #CodeReview #GitHubCopilot #ClaudeCode #Codex
