# Changelog

All notable changes to this project will be documented in this file.

The format is based on Keep a Changelog and this project uses Semantic Versioning.

## [Unreleased]

### Added

- First-class session lifecycle tools for marking items in progress, merging items, and completing sessions.
- Session filename validation for newly created sessions.
- End-to-end workflow coverage for the OBO MCP server.
- Distributable agent setup templates under `templates/agent-setup/`.
- Cross-agent setup guidance for Copilot, Codex, Claude Code, and Cline.

### Changed

- Session mutations now keep `index.json` synchronized.
- Session completion state is derived and persisted consistently.
- Package metadata and tests were cleaned up to reduce editor diagnostics.

## [0.1.0]

### Initial Release

- Initial OBO MCP server with session creation, listing, item navigation, and item update tools.
