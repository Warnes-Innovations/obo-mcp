# OBO Session Guidelines

Use the OBO MCP tools for all One-By-One review session work in this repository.

## When To Use OBO

- Use OBO when the user asks to process findings, tasks, or decisions one at a time.
- Use OBO when multiple review findings need explicit sequential approval instead of a flat summary.
- Use OBO when the item list should be resumable and persisted outside the current chat transcript.
- Prefer normal chat for small single-step tasks that do not need queue state.

## Required Workflow

- Never directly create, edit, repair, or reorder files in `.github/obo_sessions/`.
- Use `obo_list_sessions` before starting a new OBO session.
- If an incomplete session exists, ask the user whether to resume, merge, replace, or stop.
- Use `obo_create` to start a new session.
- Use `obo_merge_items` to append new findings to an existing session.
- Use `obo_next` to fetch the next actionable item.
- Use `obo_mark_in_progress` when beginning work on an item.
- Use `obo_mark_complete` or `obo_mark_skip` to resolve an item.
- Use `obo_session_status` or `obo_list_items` instead of reading `index.json` directly.
- Use `obo_complete_session` when all actionable items are resolved.

## Session Conventions

- Session files live in `.github/obo_sessions/`.
- New session filenames must follow `session_YYYYMMDD_HHMMSS.json`.
- Treat the MCP server as the source of truth for session state.

## Review Behavior

- For multiple findings, keep the OBO session updated after every user-approved action.
- For a single finding, still use the MCP session flow if the user asks for OBO handling.
- If a needed operation is not available through the MCP tools, tell the user instead of editing session JSON manually.
