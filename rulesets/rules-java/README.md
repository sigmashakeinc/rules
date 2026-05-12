# rules-java

Java governance rules for AI coding agents. Prevents SQL injection via string concatenation, XXE via unsafe XML parsers, unsafe deserialization with `ObjectInputStream`, swallowed exceptions in empty catch blocks, and abrupt JVM exits via `System.exit()` in library code.

**5 rules · 1 file**

![rules-java — AI agent Java security governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-java)


## Install

```bash
ssg hub pull rules-java
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### java_write_safety.rules (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-string-concat-sql` | DENY | error | Blocks string concat in SQL — use PreparedStatement |
| `no-xxe-vulnerable-parser` | DENY | error | Requires XXE protection on XML parsers |
| `no-java-deserialize` | DENY | error | Blocks ObjectInputStream — RCE risk |
| `no-exception-swallow` | ASK | warning | Warns on empty catch blocks |
| `no-system-exit` | ASK | warning | Warns on System.exit() in library code |

## Why this matters

Java string concatenation in SQL queries (`"SELECT * FROM users WHERE id = " + userId`) is a textbook SQL injection vulnerability — the most common security flaw in Java web applications. `ObjectInputStream.readObject()` with untrusted data is a critical RCE vector (exploited in Log4Shell-era attacks). XML parsers without XXE protection are vulnerable to server-side request forgery and file disclosure.

LLMs trained on older Java code commonly generate these vulnerable patterns. These rules block them at the moment the agent writes the code.

## Compatible with

- Java 8+, Java 11+, Java 17+ (LTS versions)
- Spring Boot, Jakarta EE, Quarkus, Micronaut
- Works alongside SpotBugs, FindBugs, and OWASP Dependency-Check — these rules operate at the agent tool-call level, not at compile time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
