# rules-ruby

Ruby and Rails governance rules for AI coding agents. Prevents `eval`, command injection with interpolated shell backticks, SQL injection in ActiveRecord queries, XSS via `raw()` and `html_safe`, and mass assignment vulnerabilities from `params.permit!` — blocking the most common Rails security anti-patterns in AI-generated code.

**5 rules · 1 file**

![rules-ruby — AI agent Ruby on Rails governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-ruby)


## Install

```bash
ssg hub pull rules-ruby
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### ruby_write_safety.rules (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-eval-ruby` | DENY | error | Blocks `eval`, `instance_eval`, `class_eval` |
| `no-system-backtick` | DENY | error | Blocks shell commands with interpolated data |
| `no-sql-string-interpolation-rails` | DENY | error | Blocks `#{}` interpolation in ActiveRecord queries |
| `no-raw-html-rails` | ASK | warning | Warns on `raw()`, `html_safe`, `<%==` in ERB |
| `no-mass-assignment-permit-all` | DENY | error | Blocks `params.permit!` — mass assignment risk |

## Why this matters

Rails applications are among the most targeted by SQL injection and mass assignment attacks — both historically common in AI-generated Rails code. `params.permit!` whitelists all parameters for mass assignment, allowing attackers to set `admin: true` or any other field. Shell backtick interpolation (`\`rm -rf #{user_input}\``) is a direct command injection path.

These rules enforce the OWASP Rails Security Guide at the AI agent tool-call level, catching vulnerabilities before they reach code review.

## Compatible with

- Ruby 2.7+, Ruby 3.x
- Rails 6.x, Rails 7.x
- Sinatra, Hanami, and plain Ruby scripts
- Works alongside Brakeman security scanner — these rules operate at the agent tool-call level, not at static analysis time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
