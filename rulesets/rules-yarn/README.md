# rules-yarn

Yarn package manager rules for AI coding agents (Classic and Berry). Enforces exact version pins (no `^` or `~` ranges), protects `yarn.lock` from manual edits, blocks hardcoded `npmAuthToken` in `.yarnrc.yml`, flags plugin installations and `resolutions` overrides, and guards `yarn publish`, `yarn unpublish`, `yarn dlx`, and `yarn patch` operations.

**9 rules · 2 files**

![rules-yarn — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-yarn)

## Install

```bash
ssg hub pull rules-yarn
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### yarn_exec_hygiene.rules — Registry and runtime operations (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-yarn-unpublish` | DENY | error | Blocks `yarn (npm) unpublish` — use `yarn npm deprecate` instead |
| `ask-yarn-publish` | ASK | warning | Confirms version, build, and .npmignore before publish |
| `ask-yarn-dlx` | ASK | warning | Flags `yarn dlx <pkg>` without `@version` — always fetches latest |
| `ask-yarn-patch` | ASK | warning | Flags `yarn patch` — must commit via `yarn patch-commit` |

### yarn_write_safety.rules — Package authoring and secrets (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-edit-yarn-lockfile` | DENY | error | Blocks hand-editing `yarn.lock` |
| `no-caret-tilde-yarn` | DENY | error | Blocks `^` and `~` version ranges — use exact pins |
| `no-yarnrc-authtoken` | DENY | error | Blocks hardcoded `npmAuthToken` in `.yarnrc.yml` — use `${NPM_AUTH_TOKEN}` |
| `ask-yarnrc-plugins` | ASK | warning | Flags plugins in `.yarnrc.yml` — execute code during yarn operations |
| `ask-yarn-resolutions` | ASK | warning | Flags `resolutions` — silently overrides transitive dep versions |

## Why this matters

Yarn Berry plugins listed in `.yarnrc.yml` execute code during every yarn operation — a malicious or compromised plugin can intercept `yarn install` or `yarn publish` silently. `resolutions` override transitive dependencies without any version compatibility checks. Hardcoded `npmAuthToken` in `.yarnrc.yml` is one of the most common credential-leak patterns in AI-managed repositories.

## Compatible with

- Yarn Classic (1.x)
- Yarn Berry (2.x, 3.x, 4.x)
- Works alongside rules-npm for projects with mixed tooling

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
