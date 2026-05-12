# rules-pnpm

pnpm package manager rules for AI coding agents. Enforces exact version pins (no `^` or `~` ranges), protects `pnpm-lock.yaml` from manual edits, blocks hardcoded tokens in `.npmrc`, flags `.pnpmfile.cjs` install hooks and `pnpm.overrides`, and guards `pnpm publish`, `pnpm unpublish`, `pnpm dlx`, and `pnpm patch` operations.

**9 rules · 2 files**

![rules-pnpm — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-pnpm)

## Install

```bash
ssg hub pull rules-pnpm
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### pnpm_exec_hygiene.rules — Registry and runtime operations (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-pnpm-unpublish` | DENY | error | Blocks `pnpm unpublish` — use `pnpm deprecate` instead |
| `ask-pnpm-publish` | ASK | warning | Confirms version, build, and .npmignore before publish |
| `ask-pnpm-dlx` | ASK | warning | Flags `pnpm dlx <pkg>` without `@version` — always fetches latest |
| `ask-pnpm-patch` | ASK | warning | Flags `pnpm patch` — patches lost on reinstall without `patch-commit` |

### pnpm_write_safety.rules — Package authoring and secrets (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-edit-pnpm-lockfile` | DENY | error | Blocks hand-editing `pnpm-lock.yaml` |
| `no-caret-tilde-pnpm` | DENY | error | Blocks `^` and `~` version ranges — use exact pins |
| `ask-pnpmfile-hooks` | ASK | warning | Flags `.pnpmfile.cjs` — executes JS on every install |
| `ask-pnpm-overrides` | ASK | warning | Flags `pnpm.overrides` — silently replaces transitive deps |
| `no-npmrc-token-pnpm` | DENY | error | Blocks hardcoded `_authToken` in `.npmrc` — use `${NPM_TOKEN}` |

## Why this matters

`.pnpmfile.cjs` silently modifies dependency resolutions on every `pnpm install` — an AI agent can introduce one without realizing it runs arbitrary code in every developer's environment. `pnpm overrides` can silently replace transitive dependency versions, masking vulnerabilities. `pnpm dlx` without version pins is a live supply-chain risk.

## Compatible with

- pnpm 8.x and 9.x
- Monorepos using pnpm workspaces
- Works alongside rules-npm for projects with mixed tooling

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
