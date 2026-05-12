# rules-secrets

Secret and credential protection rules for AI coding agents. Blocks access to `.env` files and private keys, and catches hardcoded passwords and API keys before they reach version control — preventing credential exposure in AI-generated code and agent output.

**3 rules · 1 file**

![rules-secrets — AI agent secret and credential protection demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-secrets)


## Install

```bash
ssg hub pull rules-secrets
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### fs_read_secrets.rules — Secret file and credential protection (3 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-read-env-files` | DENY | error | Blocks reading `.env`, `.env.local`, `.env.production`, etc. |
| `no-read-key-files` | DENY | error | Blocks reading `.pem`, `.key`, `*_rsa`, `credentials.json`, etc. |
| `no-hardcode-secrets` | ASK | error | Flags patterns like `password = "..."` in source code |

## What this protects against

- **Accidental exposure**: AI agents exploring a codebase may read `.env` files and inadvertently include secrets in tool output, logs, or error messages that persist in conversation context
- **Secret leakage in generated code**: LLMs sometimes generate code with hardcoded credentials from training data — this rule catches those patterns before they land in a commit
- **Supply-chain hygiene**: Private keys and credentials read by an agent could be logged, cached, or included in context that persists across sessions
- **Prompt injection via secrets**: Malicious content in `.env` files could influence agent behavior if read into context

## Compatible with

- Any project using `.env` files (dotenv, Next.js, Vite, Create React App, etc.)
- PEM certificates and SSH keys
- AWS, GCP, or Azure credential files
- TypeScript, JavaScript, Python, Ruby, Go, Java source files

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
