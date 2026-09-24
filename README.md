# Recurse

![Recurse](plugins/recurse/assets/recurse-icon.png)

**Build reusable agentic workloads.**

Your coding agent defines Python tools and checks for a task. Recurse runs an LLM around them to explore alternatives and refine results. Execution is serverless: expose the workload as an MCP server for use in agentic workflows, or run it to completion.

Use Recurse for work where trying alternatives and checking results matters: testing code changes against a benchmark, generating puzzle levels with solvability checks, or refining generated artifacts against explicit constraints.

## What you install

One Recurse skill for Cursor, Codex, and Claude Code, with each client's plugin metadata and Recurse brand assets. The skill guides your coding agent through defining tools, prompts, verification criteria, and execution with the Recurse SDK.

Recurse generates MCP deployments from your workloads. Installing this plugin does not connect a prebuilt MCP server or install the SDK. Repeated invocations do not imply persistent memory across runs.

## Requirements

- A compatible Cursor, Codex, or Claude Code installation with plugins enabled.
- Python 3.14 or newer and Recurse SDK 0.2.2 or newer.
- A Recurse account, network access, and sufficient credit for hosted execution.

In your Python environment:

```sh
pip install recurse-sdk
recurse login
```

Hosted execution uses your Recurse account and incurs usage charges. Agree on the task, success criteria, and spending allowance before running it. See [Recurse documentation](https://recurse.run/docs) and [pricing](https://recurse.run/pricing).

## Install from this repository

Download or clone this repository, then use the instructions below from its root directory. Marketplace listings are separate from installation from a checkout.

### Codex

```sh
codex plugin marketplace add .
codex plugin add recurse@synnada-recurse
```

Start a new session and select the Recurse skill. See [Codex plugin documentation](https://learn.chatgpt.com/docs/plugins).

### Claude Code

```sh
claude plugin marketplace add .
claude plugin install recurse@synnada-recurse --scope user
```

Start a new session and invoke `/recurse:recurse`. See [Claude Code marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces).

### Cursor

Copy `plugins/recurse` into `~/.cursor/plugins/local/recurse`, then restart Cursor. Open **Customize → Plugins → Recurse** and check that its skill is available. If that folder already exists, preserve the previous copy before replacing it with the new package.

Cursor 3.20.17 displays the local plugin's logo, version, and website but omits its description. This does not prevent the skill from loading. See [Cursor plugin documentation](https://cursor.com/docs/plugins).

## Try it

- Design a Python workload that tests code changes against a benchmark.
- Plan a Recurse workload that generates puzzle levels and checks solvability.
- Help me expose a tested Recurse workload through MCP.

Review the proposed workload and its checks before hosted execution. Ask your coding agent to inspect the terminal status, completion receipt, and saved artifacts before reporting success. An execution finishing normally does not by itself establish that your acceptance criteria were met.

For a generated MCP deployment, follow the [deployment guide](https://recurse.run/docs/deploy). In Cursor, confirm the intended workspace MCP source is enabled and connected under **Customize → MCPs** before invoking it.

## Update

Update your checkout to the desired release. For Codex, run `codex plugin add recurse@synnada-recurse` again. For Claude Code, run `claude plugin update recurse@synnada-recurse --scope user`. For Cursor, replace the local plugin folder with the reviewed new package. Start a new session after an update.

Each release bundles a fixed snapshot of the [website skill](https://recurse.run/SKILL.md). An installed copy changes when you update the plugin; it does not fetch new instructions automatically during use.

## Links and licensing

Plugin instructions, metadata, and documentation are licensed under Apache 2.0. Recurse logos are covered by separate brand-asset terms; see [Licensing](LICENSING.md).

[Website](https://recurse.run) · [Documentation](https://recurse.run/docs) · [Release notes](CHANGELOG.md) · [Licensing](LICENSING.md)
