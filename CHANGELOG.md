# Release notes

## 0.4.0 — 2026-10-14

- Extend Recurse guidance with approved API discovery and private Python authoring, source upload, execution, exact replay, and cancellation through 13 generic MCP operations.
- Document one allowance for preparation, API charges at 1×, and compute at 4×; keep credentials in the trusted parent.
- Keep API schemas and price ceilings in the live server catalog so new approved endpoints need no package release.
- Require Recurse SDK 0.2.6 or newer for native Tools use; production services are the default, with explicit TEST settings documented separately.
- Preserve Recurse Agents instructions, configuration, starter prompts, assets, and licensing. Its manifest version alone follows the shared 0.4.0 release.
- Prepare OpenAI upload archives separately from the native stdio packages; Portal upload, review, and publication remain separate owner actions.

## 0.3.0 — 2026-10-14

- Rename the existing agent-authoring package and skill to Recurse Agents (`recurse-agents`), preserving the current agent instructions and prompt examples.
- Include the native run trace guidance already present in canonical website main ([web #229](https://github.com/synnada-ai/recurse-web/pull/229)); the legacy website skill stays unchanged.
- Add Recurse (`recurse`) for consumer Tools discovery, inspected calls, stored results, and cancellation through five stable operations.
- Use the separate `synnada-recurse-plugins` marketplace and document migration from the legacy agent selector. Distinct cached identities were verified with Codex CLI 0.151.0; other host migration checks remain separate.
- Synchronize both packages' four manifests at 0.3.0, copy OpenAI presentation metadata into the portable manifests, and reuse the existing brand assets and licensing.
- Wire native Tools through `recurse tools mcp serve`; remote OpenAI upload candidates and production publication are prepared separately.

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
