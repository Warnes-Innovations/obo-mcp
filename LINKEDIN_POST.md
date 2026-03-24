<!--
Copyright (C) 2026 Gregory R. Warnes
SPDX-License-Identifier: AGPL-3.0-or-later

This file is part of Oboe MCP.
For commercial licensing, contact greg@warnes-innovations.com
-->

# Coding Agents Need Workflow State, Not Just Chat

If you use LLM coding agents, you have probably had this painful experience:

> The agent finds 8 issues, fixes 2, forgets 1, loses track of a blocker, and after a reload or restart you are left reconstructing what happened from chat.

That is not really a reasoning problem. It is a workflow problem.

We built `oboe-mcp` around One-by-One review sessions to solve exactly that problem.

I just used `oboe-mcp` One-by-One sessions to manage a large refactor, breaking a 10,451-line monolith into 27 focused modules without losing track of what was done, what was blocked, and what still needed review.

Instead of treating the transcript as the system of record, the agent keeps a durable session with:

- items ordered by priority and dependency
- explicit lifecycle state (pending, blocked, deferred, completed, etc.)
- a record of what was accepted or rejected and why
- child sessions for side investigations
- resumable history another agent can pick up later

For software developers using LLM agents, that means:

- no more "walls of text" for questions, decisions, or conclusions
- clearer one-at-a-time review and approval flow
- less duplicated review after context loss
- easier task resumption and handoff between sessions, reloads, or even different agents
- a clear record of what was reviewed, approved, skipped, blocked, and completed

`oboe-mcp` is open source and works out-of-the-box with Copilot, Codex, Claude Code, and Cline.

It includes the MCP server plus agent instructions, prompts, and skill templates that tell agents when to use the One-by-One workflow. It also has an install script that knows where to place the agent-specific files, which reduces manual setup.

*If you use coding agents for multi-step work, make your life easier by trying the One-by-One workflow: [github.com/Warnes-Innovations/oboe-mcp](https://github.com/Warnes-Innovations/oboe-mcp)*

Hashtags: #MCP #AIAgents #DeveloperTools #CodeReview #LLM #GitHubCopilot #ClaudeCode #Codex #Cline
