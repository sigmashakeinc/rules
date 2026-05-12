# rules-c

C language security governance rules for AI coding agents. Blocks the most dangerous unsafe C functions: gets() (guaranteed buffer overflow), sprintf() without bounds, strcpy()/strcat() (buffer overflow), unbounded scanf("%s"), system() with user input (command injection), format string vulnerabilities via printf(user_input), and malloc() without null checks.

**7 rules · 1 file**

![rules-c — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-c)

## Install

```bash
ssg hub pull rules-c
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### c_write_safety.rules — Security (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-gets` | DENY | error | Bans `gets()` — removed from C11, buffer overflow |
| `no-sprintf-no-bound` | ASK | error | Flags `sprintf()` — use `snprintf()` |
| `no-strcpy-strcat` | ASK | error | Flags `strcpy()`/`strcat()` — use size-bounded variants |
| `no-scanf-unbounded` | ASK | error | Flags `scanf("%s")` without width limit |
| `no-system-with-user-input` | ASK | error | Flags `system()`/`popen()` with variables |
| `no-format-string-user-input` | DENY | error | Blocks `printf(user_var)` — format string vuln |
| `no-malloc-without-null-check` | LOG | warning | Flags malloc without null check |

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
