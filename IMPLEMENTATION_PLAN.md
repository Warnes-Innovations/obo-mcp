# OBO MCP Implementation Plan

## Scope

Close the remaining workflow gaps that still push agents toward direct JSON edits.

## Goals

1. Support the full session lifecycle through MCP tools.
2. Keep `index.json` consistent with session mutations.
3. Make common workflow actions discoverable as first-class tools.
4. Align documentation with actual behavior.
5. Add regression tests for the recovered gaps.

## Priority Order

### Phase 1: Session lifecycle correctness

1. Ensure item mutations keep `index.json` synchronized.
2. Add explicit support for marking items `in_progress`.
3. Add support for closing a session when work is complete.

### Phase 2: Resume and merge workflows

1. Add a tool to append new items to an existing session.
2. Allow reopening a completed session when items are merged in.

### Phase 3: Documentation and validation

1. Document the new workflow surface in the README.
2. Enforce or clearly document session filename rules.
3. Add tests covering the intended agent workflow.

## Patch List

### 1. `src/obo_mcp/session.py`

- Add a helper to update session-level status based on item states.
- Update `update_field()` to refresh `index.json` after changes.
- Add `mark_in_progress()`.
- Add `merge_items()` for appending normalized items to an existing session.
- Add `complete_session()` for explicit session closure.
- Reopen completed sessions automatically when merged items are added.
- Recompute session status after relevant item-level mutations.
- Optionally validate session filenames against the documented pattern.

### 2. `src/obo_mcp/server.py`

- Register a first-class `obo_mark_in_progress` MCP tool.
- Register a first-class `obo_merge_items` MCP tool.
- Register a first-class `obo_complete_session` MCP tool.
- Return structured JSON responses consistent with existing tools.

### 3. `tests/test_session.py`

- Add regression tests for index updates after `update_field()`.
- Add tests for `mark_in_progress()`.
- Add tests for explicit session completion.
- Add tests for automatic session status transitions.
- Add tests for merging items into active and completed sessions.

### 4. `tests/test_server.py`

- Add handler tests for the new MCP tools.
- Add integration coverage for a realistic agent flow:
  create -> next -> mark_in_progress -> merge_items -> complete item(s) -> complete session.

### 5. `README.md`

- Update the advertised tool count and table.
- Document the first-class lifecycle tools.
- Document merge/resume behavior.
- Clarify whether session filenames are validated or only conventional.

## Design Notes

- Keep public return shapes simple JSON objects to match the current server style.
- Preserve existing tool names and semantics where possible.
- Prefer session-level helper functions in `session.py` so `server.py` stays thin.
- Avoid silent index drift: every mutating operation should update `index.json`.
- Treat `completed` as a session-level state, not just an item aggregate.

## Initial Execution Plan

1. Implement session-layer helpers and fix index synchronization.
2. Add MCP tools for `in_progress`, `complete_session`, and `merge_items`.
3. Add regression tests for each new mutation path.
4. Update README to reflect the shipped surface.
5. Run targeted pytest coverage for server and session tests.

## Commit Strategy

1. Commit this plan document alone.
2. Implement the session lifecycle fixes and new tools.
3. Validate with focused tests before any further commit.
