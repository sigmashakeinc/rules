# rules-kotlin

Kotlin/Android security governance rules for AI coding agents. Blocks force non-null assertions that cause NPEs, SQL string interpolation, Java deserialization (RCE), command injection via Runtime.exec(), hardcoded credentials, unsafe unchecked casts, and cleartext HTTP in production.

**7 rules · 1 file**

![rules-kotlin — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-kotlin)

## Install

```bash
ssg hub pull rules-kotlin
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### kotlin_write_safety.rules — Security (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-force-non-null-kotlin` | ASK | warning | Flags `!!` — use `?.` or `?:` |
| `no-sql-concat-kotlin` | DENY | error | Blocks SQL string concat/interpolation |
| `no-java-deserialization-kotlin` | DENY | error | Bans ObjectInputStream — RCE risk |
| `no-runtime-exec-kotlin` | ASK | error | Flags Runtime.exec() with interpolation |
| `no-hardcoded-secrets-kotlin` | ASK | error | Flags hardcoded credentials |
| `no-unchecked-cast-kotlin` | ASK | warning | Flags unsafe `as` casts — use `as?` |
| `no-cleartext-http-kotlin` | ASK | error | Flags http:// in production code |

## Compatible with

- Kotlin 1.8+, Android SDK 21+
- Spring Boot, Ktor, Exposed
- Works alongside detekt and Android Lint

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
