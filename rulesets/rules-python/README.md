# rules-python

Python governance rules for AI coding agents. Blocks code injection via `eval()` and `exec()`, command injection via `os.system()` and `shell=True`, unsafe deserialization with `pickle.loads()`, SQL injection via f-string formatting, and `yaml.load()` without safe loader — preventing the most critical Python security vulnerabilities in AI-generated code.

**11 rules · 2 files**

![rules-python — AI agent Python security governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-python)


## Install

```bash
ssg hub pull rules-python
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### py_write_safety.rules — Security (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-eval-exec` | DENY | error | Bans `eval()` and `exec()` — arbitrary code execution |
| `no-os-system` | DENY | error | Bans `os.system()` and `os.popen()` — use subprocess |
| `no-shell-true` | DENY | error | Bans `shell=True` in subprocess — injection risk |
| `no-pickle-loads` | DENY | error | Bans `pickle.loads()` — RCE with untrusted data |
| `no-sql-string-format` | DENY | error | Blocks f-string/% formatting in SQL queries |
| `no-yaml-load-unsafe` | DENY | error | Requires `yaml.safe_load()` not `yaml.load()` |
| `no-assert-for-validation` | ASK | warning | Warns against assert for input validation |

### py_write_style.rules — Code quality (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-bare-except` | DENY | error | Bans bare `except:` — catch specific exceptions |
| `no-mutable-default-arg` | ASK | warning | Warns on `def f(x=[])` — mutable default args |
| `no-print-in-src` | LOG | warning | Flags `print()` in src/ — use logging module |
| `no-wildcard-import` | ASK | warning | Flags `from module import *` |

## Why this matters

Python's dynamic nature makes it particularly vulnerable to AI-generated security issues. `eval()` and `exec()` with unsanitized input enable arbitrary code execution. `pickle.loads()` with untrusted data is a well-known RCE vector (CVE-level in Django, Flask, and ML frameworks). `shell=True` in `subprocess` turns any string interpolation into a command injection vulnerability.

These rules catch the patterns that Bandit and pylint miss — because they fire at the agent tool-call level, before the code is even written to disk.

## Compatible with

- Python 3.8+
- Django, Flask, FastAPI, Starlette, Tornado
- SQLAlchemy, psycopg2, sqlite3
- Works alongside Bandit, Semgrep, and pylint — these rules operate at the agent tool-call level, not at lint time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
