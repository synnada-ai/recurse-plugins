# Release notes

## 0.2.3 — 2026-09-17

- Correct CLI exit-code guidance: `2` means a confirmed remote timeout; invalid command syntax and other CLI errors use `1`.
- Add troubleshooting guidance to upgrade the SDK, refresh the skill, and consult the documentation.
- Clarify agent degrees of freedom and one-off execution wording.

## 0.2.2 — 2026-09-14

- Recurse skill for Cursor, Codex, and Claude Code.
- Guidance for defining Python tools, evaluating hypotheses, preserving the best feasible result, and checking completion and artifacts.
- Serverless execution with two paths: expose a workload as MCP or run it to completion.
- Recurse logos and platform-specific plugin metadata.
- Apache 2.0 licensing for plugin instructions, metadata, and documentation, with separate terms for the bundled Recurse logos.
- Canonical skill correction: the built-in tool flag is `tools.built_in`.
