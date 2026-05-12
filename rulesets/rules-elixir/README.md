# rules-elixir

Elixir/Phoenix security governance rules for AI coding agents. Blocks Code.eval_string() RCE, command injection via System.cmd with string concatenation, SQL fragment injection in Ecto queries, atom exhaustion from String.to_atom with user input, hardcoded secrets in config, and unsafe :erlang.binary_to_term deserialization.

**6 rules · 1 file**

![rules-elixir — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-elixir)

## Install

```bash
ssg hub pull rules-elixir
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### elixir_write_safety.rules — Security (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-code-eval-elixir` | DENY | error | Bans `Code.eval_string()` — RCE |
| `no-system-cmd-injection` | ASK | error | Flags `System.cmd` with string concat |
| `no-sql-fragment-ecto` | DENY | error | Blocks Ecto fragment with `<>` concat |
| `no-string-to-atom-user-input` | DENY | error | Blocks `String.to_atom()` with user input |
| `no-hardcoded-secrets-elixir` | ASK | error | Flags hardcoded secrets in config |
| `no-unsafe-deserialization-elixir` | DENY | error | Blocks `:erlang.binary_to_term/1` without :safe |

## Compatible with

- Elixir 1.14+, Erlang/OTP 25+
- Phoenix, Ecto, Plug
- Works alongside Credo and Sobelow

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
