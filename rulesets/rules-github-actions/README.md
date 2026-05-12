# rules-github-actions

GitHub Actions workflow security governance rules for AI coding agents. Blocks the most critical CI/CD security misconfigurations: expression injection via github.event context in run steps, pull_request_target with unsafe checkout (supply chain RCE), hardcoded secrets in workflow files, write-all permissions, unpinned action versions (supply chain attacks), and self-hosted runners on public repo PRs.

**6 rules · 1 file**

![rules-github-actions — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-github-actions)

## Install

```bash
ssg hub pull rules-github-actions
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### gha_write_safety.rules — Security (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-expression-injection-gha` | DENY | error | Blocks github.event.* injection in run steps |
| `no-pull-request-target-checkout` | DENY | error | Blocks pull_request_target + actions/checkout |
| `no-hardcoded-secrets-gha` | DENY | error | Blocks hardcoded credentials in workflows |
| `no-write-all-permissions` | ASK | error | Flags write-all GITHUB_TOKEN permissions |
| `no-unpinned-action-version` | ASK | warning | Flags branch/tag refs — use commit SHAs |
| `no-self-hosted-runner-public-repo` | ASK | error | Flags self-hosted runners on PR triggers |

## Compatible with

- GitHub Actions (all runners)
- Works alongside StepSecurity Harden Runner, actionlint, and Zizmor

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
