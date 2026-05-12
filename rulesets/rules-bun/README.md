# rules-bun

Bun package manager rules for AI coding agents. Enforces exact version pins (no `^` or `~` ranges), protects `bun.lock` and `bun.lockb` from manual edits, blocks hardcoded registry tokens in `bunfig.toml`, flags `trustedDependencies` supply-chain grants, guards `bun publish`, and prevents unversioned `bunx` execution.

**7 rules · 2 files**

![rules-bun — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-bun)

## Install

```bash
ssg hub pull rules-bun
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### bun_exec_hygiene.rules — Runtime and publish operations (3 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `ask-bun-publish` | ASK | warning | Confirms version, build, and files before `bun publish` |
| `ask-bunx-unversioned` | ASK | warning | Flags `bunx <pkg>` without `@version` — always fetches latest |
| `ask-bun-patch` | ASK | warning | Flags `bun patch` — patches lost on reinstall without `--commit` |

### bun_write_safety.rules — Package authoring and secrets (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-edit-bun-lockfile` | DENY | error | Blocks hand-editing `bun.lock` / `bun.lockb` |
| `no-caret-tilde-bun` | DENY | error | Blocks `^` and `~` version ranges — use exact pins |
| `no-bunfig-token` | DENY | error | Blocks hardcoded tokens in `bunfig.toml` — use `$BUN_AUTH_TOKEN` |
| `ask-bun-trusted-dependencies` | ASK | warning | Flags `trustedDependencies` — each entry is a postinstall trust grant |

## Why this matters

AI agents working in Bun projects routinely add `^` version ranges (the npm default), making builds non-reproducible. `bunx` without a pinned version always fetches the latest release of a package — a compromised maintainer account can push malicious code that executes immediately. `trustedDependencies` in `package.json` is a supply-chain trust decision that should always be a deliberate human choice.

## Compatible with

- Bun 1.x projects (Node.js compatible)
- Works alongside rules-npm for projects using both npm and bun tooling

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
