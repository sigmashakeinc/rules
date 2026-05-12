# rules-go

Go language governance rules for AI coding agents. Catches ignored errors, unsafe pointer packages, goroutine leaks, naming violations, and concurrency hazards — enforcing production-grade Go patterns in AI-generated code.

**15 rules · 3 files**

![rules-go — AI agent Go language governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-go)


## Install

```bash
ssg hub pull rules-go
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### go_write_safety.rules — Error handling & security (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-ignored-errors` | DENY | error | Flags silently discarded function errors |
| `no-panic-in-library` | ASK | warning | Warns on panic() in non-main library code |
| `no-unsafe-package` | ASK | warning | Flags `import "unsafe"` usage |
| `no-sql-sprintf` | DENY | error | Blocks `fmt.Sprintf` in SQL queries |
| `no-goroutine-without-wg` | LOG | warning | Logs goroutine spawns without WaitGroup |

### go_write_style.rules — Naming & code style (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-unexported-type-in-public-api` | ASK | warning | Public function exposing unexported type |
| `no-stuttering-package-names` | LOG | warning | Flags stuttering names like `http.HTTPServer` |
| `no-exported-func-without-comment` | LOG | info | Exported function missing godoc comment |
| `no-naked-return` | ASK | warning | Bare `return` in named-return functions |
| `no-single-letter-var-outside-loop` | LOG | info | Single-letter variable names outside loops |

### go_write_concurrency.rules — Concurrency safety (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-mutex-copy` | DENY | error | Blocks copying sync.Mutex after first use |
| `no-channel-without-close` | LOG | warning | Logs channels that may not be closed |
| `no-context-in-struct` | ASK | warning | context.Context stored in struct field |
| `no-select-without-default-or-timeout` | LOG | warning | select without timeout or context cancellation |
| `no-time-sleep-in-production` | ASK | warning | time.Sleep() in non-test code |

## Why this matters

LLMs frequently generate Go code that silently ignores errors (`_ = f()`) — a critical Go anti-pattern that causes silent failures in production. Goroutine leaks from ungrouped spawns, copying mutexes by value, and `fmt.Sprintf` SQL queries are also common LLM output patterns that pass compilation but cause runtime bugs or security vulnerabilities.

These rules enforce idiomatic, production-ready Go at the agent tool-call level — catching issues that `go vet` doesn't cover.

## Compatible with

- Go 1.18+
- Any Go project (services, CLIs, libraries)
- Works alongside `go vet` and `golangci-lint` — these rules operate at the agent tool-call level, not at build time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
