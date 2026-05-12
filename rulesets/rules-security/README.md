# rules-security

Cross-language OWASP Top 10 security rules for AI coding agents. Blocks hardcoded passwords, broken cryptography (MD5, SHA-1), insecure random number generation, CORS misconfiguration, disabled TLS verification, and XML external entity (XXE) injection.

**6 rules · 1 file**

![rules-security — AI agent OWASP security governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-security)


## Install

```bash
ssg hub pull rules-security
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### security_write_owasp.rules (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-hardcoded-password` | DENY | error | Blocks hardcoded passwords in TS/JS/Python/Java/Go |
| `no-md5-sha1-crypto` | ASK | warning | Warns on broken crypto (MD5, SHA-1) for security use |
| `no-insecure-random` | DENY | error | Blocks `Math.random()` for tokens/secrets |
| `no-cors-wildcard-with-credentials` | DENY | error | Blocks CORS `*` + credentials combo |
| `ask-disable-ssl-verify` | ASK | error | Flags disabled TLS verification |
| `no-xml-external-entities` | DENY | error | Blocks unsafe XML parsers (XXE risk) |

## OWASP Coverage

| OWASP Top 10 | Rules Covering It |
|---|---|
| A01 Broken Access Control | `no-iam-star-permissions` (see rules-aws) |
| A02 Cryptographic Failures | `no-md5-sha1-crypto`, `no-insecure-random` |
| A03 Injection | `no-hardcoded-password`, `no-xml-external-entities` |
| A05 Security Misconfiguration | `no-cors-wildcard-with-credentials`, `ask-disable-ssl-verify` |
| A07 Identification Failures | `no-hardcoded-password` |

## Why this matters

LLMs frequently generate code with `Math.random()` for token generation, MD5 for password hashing, and `verify: false` for TLS — patterns that were common in older training data but are security vulnerabilities in production. `CORS: '*' + credentials: true` is a particularly common misconfiguration that bypasses browser security.

These rules apply to any language — TypeScript, JavaScript, Python, Java, Go — making them the broadest security layer in the SigmaShake Hub ruleset collection.

## Compatible with

- TypeScript, JavaScript, Python, Java, Go (cross-language pattern matching)
- Any web framework (Express, FastAPI, Spring, Gin, etc.)
- Works alongside SAST tools like Semgrep and Snyk — these rules operate at the agent tool-call level

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
