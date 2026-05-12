# rules-git

Git safety and hygiene rules for AI coding agents. Prevents history rewrites (`--force`, `--hard`), protects against accidental secret commits, and enforces safe branch workflows — stopping irreversible git operations before they execute.

**11 rules · 2 files**

![rules-git — AI agent git safety governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-git)


## Install

```bash
ssg hub pull rules-git
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### git_exec_safety.rules — Destructive operation prevention (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-force-push` | DENY | error | Blocks `git push --force` and `-f` — rewrites shared history |
| `no-hard-reset` | DENY | error | Blocks `git reset --hard` — permanently discards changes |
| `no-git-clean-force` | DENY | error | Blocks `git clean -f` — permanently deletes untracked files |
| `ask-branch-delete-force` | ASK | warning | Prompts before `git branch -D` force deletion |
| `ask-rebase` | ASK | warning | Confirms rebase is on a local/personal branch |
| `ask-checkout-destructive` | ASK | warning | Flags `git checkout --` and `git restore .` |

### git_exec_hygiene.rules — Commit content safety (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-commit-env-files` | DENY | error | Blocks staging `.env`, `credentials`, `.secret` files |
| `no-commit-node-modules` | DENY | error | Blocks staging `node_modules/` |
| `no-commit-temp-files` | DENY | error | Blocks staging `.log`, `.tmp`, `.bak`, `.swp` files |
| `ask-amend-commit` | ASK | warning | Confirms amend is safe before rewriting history |
| `log-merge-commit` | LOG | info | Logs merge commits for awareness |

## Why this matters

AI agents commit and push code automatically. Without guardrails, a single `git push --force` can overwrite teammates' work on a shared branch, and `git reset --hard` silently discards uncommitted changes with no undo. Secret files like `.env` are frequently staged by accident when an agent uses `git add -A`.

- **History protection**: Force-push and hard-reset blocks preserve shared branch history
- **Secret prevention**: Blocks `.env`, credential files, and private keys from reaching version control
- **Safe workflow**: ASK rules require human confirmation before rebasing or amending published commits

## Compatible with

- Git 2.x+
- Any git hosting (GitHub, GitLab, Bitbucket, Azure DevOps)
- Works alongside pre-commit hooks and branch protection rules — these rules intercept tool calls before git runs

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
