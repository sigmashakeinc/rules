# rules-pip

Python package manager rules for AI coding agents (pip and uv). Blocks `--trusted-host` TLS bypass, flags dependency confusion vectors (`--extra-index-url`, `--index-url`), enforces pinned versions in `requirements.txt`, protects `uv.lock` from manual edits, and blocks credentials in `.pypirc` and `pip.conf`.

**8 rules · 2 files**

![rules-pip — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-pip)

## Install

```bash
ssg hub pull rules-pip
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### pip_exec_hygiene.rules — Install and publish operations (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-pip-trusted-host` | DENY | error | Blocks `--trusted-host` — disables TLS verification |
| `ask-pip-extra-index` | ASK | warning | Flags `--extra-index-url` / `--index-url` — dependency confusion risk |
| `ask-uv-publish` | ASK | warning | Confirms version and artifacts before `uv publish` |
| `ask-pip-upgrade-unpinned` | ASK | warning | Flags `pip install --upgrade` without a version pin |

### pip_write_safety.rules — Dependency pinning and secrets (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-unpinned-requirements` | DENY | error | Blocks bare package names in `requirements.txt` — use `==version` |
| `no-pypirc-password` | DENY | error | Blocks plaintext password in `.pypirc` — use API tokens |
| `no-edit-uv-lockfile` | DENY | error | Blocks hand-editing `uv.lock` |
| `no-pip-conf-credentials` | DENY | error | Blocks passwords/tokens in `pip.conf` |

## Why this matters

`--extra-index-url` is the leading cause of dependency confusion attacks in Python projects: pip installs the highest version found across all indexes, so a public `requests==99.0.0` package on PyPI beats a private `requests==1.0.0` on an internal index. `--trusted-host` silently disables TLS verification for an entire domain. AI agents writing `requirements.txt` without version pins make every install non-reproducible and vulnerable to supply-chain attacks.

## Compatible with

- pip (22+)
- uv 0.4+
- pipenv, Poetry (partial — lockfile and credential rules apply)
- Python 3.8+

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
