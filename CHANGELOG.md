# Release notes

## 0.2.7 — 2026-09-24

- Restore the 512 MiB minimum run memory ceiling and recommend SDK 0.2.3, which accepts it locally; the default remains 1024 MiB.

## 0.2.6 — 2026-09-24

- Match the new 768 MiB minimum run memory ceiling and recommend SDK 0.2.2, which validates it locally; the default remains 1024 MiB.

## 0.2.5 — 2026-09-24

- Synchronize the coding-agent skill with the released website and Recurse SDK 0.2.1.
- Explain account-funded runs, the provider execution limit, direct-run `--non-preemptible`, checkpoint recovery, GPT-6 model selection, the `task` input, and the 0/1/130 CLI exit behavior.

## 0.2.4 — 2026-09-18

- Adopt the agreed CLI exit-code table: `1` confirmed agent failure, `2` every CLI-layer error, `3` confirmed cancellation, `4` confirmed infrastructure failure, `5` confirmed agent timeout, `130` Ctrl-C. Requires recurse-sdk 0.1.8 (synnada-ai/recurse-sdk#47).

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
