# Recurse plugins

![Recurse](plugins/recurse/assets/recurse-icon.png)

Two plugins by Synnada, version **0.4.0**.

| Plugin | Use it for | Skill |
| --- | --- | --- |
| **Recurse** (`recurse`) | Discover approved APIs and hosted tools; write and privately execute Python within an allowance; read durable results and charges. | `recurse` |
| **Recurse Agents** (`recurse-agents`) | Define Python tools, prompts, and verifiers; build, run, and deploy custom agents. | `recurse-agents` |

The server catalogs are authoritative. Their contents can change without a plugin release. The Tools plugin connects 13 generic operations: `catalog_search`, `catalog_get`, `call`, `get_call`, `cancel_call`, `apis_search`, `apis_get`, `private_stage`, `private_complete`, `private_get_version`, `private_inspect`, `private_replay`, and `private_call`. Responses are ordinary MCP results; pending calls are followed through `get_call`. Private source uses a scoped HTTP upload rather than archive bytes or local paths inside MCP frames.

Recurse Agents preserves the existing agent-authoring guidance. It has no preconfigured MCP server; deploying a tested agent creates a separate connection for that agent.

## Requirements

- A compatible Codex, Claude Code, or Cursor installation with plugins enabled.
- Python 3.14 or newer and a Recurse account.
- For Tools, Recurse SDK 0.2.6 or newer provides `recurse tools mcp serve` and private Python execution. Install or update it with `pip install -U recurse-sdk`, then check `recurse tools --help` before connecting. This checkout does not install the SDK.
- For Agents, Recurse SDK 0.2.3 or newer.
- Network access and sufficient account credit for paid work.

Authenticate explicitly with `recurse login` before connecting. The Tools bridge uses the existing login and does not open a browser automatically. Keep credentials out of plugin files. Hosted calls can incur charges: inspect the current price and agree on an allowance before submitting work.

## Migrate an existing agent plugin

Earlier releases used `recurse@synnada-recurse` for agent authoring. The new marketplace is `synnada-recurse-plugins`; the old selector must not be repointed to Tools. A version bump or a different ZIP filename does not migrate an existing installation.

Also inspect any standalone agent skill installed from the legacy `/SKILL.md` URL or the older private `recurse@personal` catalog. Keep that guidance until Agents is verified, then disable or remove its old discovery entry before installing Tools.

1. Add this checkout as a separate marketplace and install `recurse-agents@synnada-recurse-plugins`.
2. Start a new session. Verify **Recurse Agents**, version 0.4.0, and the `recurse-agents` skill with the existing agent workflow.
3. Disable or remove the legacy `recurse@synnada-recurse` agent plugin using the host's supported plugin controls. Preserve its catalog and cached package until the new installation is verified.
4. Install `recurse@synnada-recurse-plugins` for Tools. Start a new session and verify **Recurse**, version 0.4.0, and exactly one `recurse-tools` server.

Codex CLI 0.151.0 verified distinct cached identities for the released legacy package and the new Agents package, followed by removal of the legacy plugin and installation of Tools. A fresh bundled Codex 0.162.0-alpha.17.2 session loaded both skills and inspected the live TEST catalog. Refreshing the old Git marketplace against the new catalog failed on the name mismatch and preserved its cached Agent snapshot. Claude manifests passed strict validation; Claude and Cursor behavior still need owner UAT. If adding the new source replaces the legacy identity or its instructions, stop the migration and keep the legacy installation separate.

## Install from a checkout

Run these commands from the repository root. Choose either plugin or both; marketplace publication is a separate step.

### Codex

```sh
codex plugin marketplace add .
codex plugin add recurse-agents@synnada-recurse-plugins
codex plugin add recurse@synnada-recurse-plugins
```

Start a new session after installation. See [official OpenAI plugin documentation](https://developers.openai.com/plugins/build/plugins).

### Claude Code

```sh
claude plugin marketplace add .
claude plugin install recurse-agents@synnada-recurse-plugins --scope user
claude plugin install recurse@synnada-recurse-plugins --scope user
```

Start a new session and invoke `/recurse-agents:recurse-agents` for agent authoring or `/recurse:recurse` for Tools. See [Claude Code plugin documentation](https://code.claude.com/docs/en/plugins-reference).

### Cursor

Copy the chosen package into its own local directory:

- `plugins/recurse-agents` → `~/.cursor/plugins/local/recurse-agents`
- `plugins/recurse` → `~/.cursor/plugins/local/recurse`

Before replacing an existing `recurse` directory, preserve and disable the legacy agent package, then verify the new Agents package. Restart Cursor and check the skills and MCP connection under **Customize**. See [Cursor plugin documentation](https://cursor.com/docs/reference/plugins).

## Connection formats

The native Tools package launches `recurse` with arguments `["tools", "mcp", "serve"]` over stdio. The package contains no fixed service URL or secrets; the SDK uses production by default. For TEST, pass `RECURSE_API_URL=https://api.dev.recurse.run` and `RECURSE_TOOLS_URL=https://tools.dev.recurse.run` through the host's supported MCP environment settings. Codex filters ambient variables for MCP subprocesses; setting them only in the parent shell is insufficient. Historical M5 TEST UAT used a per-session environment override with the unchanged command and arguments and verified one effective connection.

Portable hosts use root `mcp.json`, including the Agent Plugins schema and explicit `type: "stdio"`. Compatibility manifests point to `.mcp.json`, which uses the host's command-based format. Both files contain one server named `recurse-tools`. Cursor's explicit `mcpServers` path overrides automatic `mcp.json` discovery; Claude Code merges the default and declared configuration by server name. OpenAI's root `extensions.com.openai` replaces its compatibility overlay, so the complete interface is copied into both. See the [OpenAI](https://developers.openai.com/plugins/build/plugins), [Claude Code](https://code.claude.com/docs/en/plugins-reference), and [Cursor](https://cursor.com/docs/reference/plugins) format references. Confirm one effective connection in the host; do not add a second manual Tools server.

OpenAI upload archives are prepared separately with a verified remote HTTPS endpoint and OAuth. This native stdio checkout is not an OpenAI upload artifact. Portal review and publication remain separate steps.

## Private Python tools

Use Recurse SDK 0.2.6 or newer and sign in explicitly with `recurse login`. Production is the default. For TEST UAT, use the TEST endpoint variables above through the host's MCP environment configuration.

Discover APIs with `apis_search`, inspect the live schemas and ceilings with `apis_get`, then declare their returned IDs in the function's optional `apis` list in `tools.yaml`. Call them in Python through `from recurse_apis import call`. A private execution permits up to 20 sequential requests and keeps upstream credentials outside the network-blocked Python sandbox. Provider charges pass through at 1×; compute is 4× its cost basis. The approved cap covers preparation and execution, including API requests. Never increase it silently.

The SDK exposes private staging, completion, preparation, and execution through `ToolsClient`. The CLI is `recurse tools run ./project --function FUNCTION --inputs inputs.json --idempotency-key REQUEST_KEY --max-cost-micro-usd APPROVED_CAP`. Remote clients use the generic private operations, build a real source archive, and transfer it over the returned scoped HTTP grant; a local path is not a remote upload. Read stored receipts to establish completion, charges, and confirmed cancellation. Publication remains restricted to the pinned operator account.

A newly approved read API is a server catalog change. An agent discovers its live schema and declares the returned ID; it needs no new plugin version for that endpoint. Changes to connection configuration or these instructions still require a reviewed package release.

## Try and update

For Tools, ask: “Find a tool for my task and inspect its inputs and price.” Check that the tool and price versions, finite JSON inputs, cap, and retry key are explicit before a call. Retain the receipt and read the existing call to follow progress, results, and billing. Cancellation requests do not establish termination or released funds.

For Agents, ask: “Design a Python workload that tests code changes against a benchmark.” Review the proposal, independent checks, and allowance before hosted execution. Inspect terminal status, completion evidence, and artifacts before claiming success.

Each release bundles fixed canonical snapshots: [Tools skill](https://recurse.run/tools/SKILL.md) and [Agents skill](https://recurse.run/agents/SKILL.md). The [legacy skill URL](https://recurse.run/SKILL.md) continues to contain agent guidance during migration. Installed instructions change only when the package is updated.

Update the checkout, use the host's supported plugin update control for the selected new identity, and start a new session. Keep the old marketplace selector separate throughout migration.

## Links and licensing

Instructions, metadata, and documentation are licensed under Apache 2.0. Recurse logos retain their separate brand-asset terms; see [Licensing](LICENSING.md).

[Website](https://recurse.run) · [Documentation](https://recurse.run/docs) · [Release notes](CHANGELOG.md) · [Licensing](LICENSING.md)
