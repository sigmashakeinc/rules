# rules-scala

Scala security governance rules for AI coding agents. Blocks Java ObjectInputStream deserialization (RCE), SQL string interpolation injection, command injection via Runtime.exec() with concatenation, unsafe asInstanceOf casts, hardcoded credentials, and XXE via scala.xml.XML.load.

**6 rules · 1 file**

![rules-scala — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-scala)

## Install

```bash
ssg hub pull rules-scala
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### scala_write_safety.rules — Security (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-java-deserialize-scala` | DENY | error | Bans `ObjectInputStream` — Java deserialization RCE |
| `no-sql-interpolation-scala` | DENY | error | Blocks SQL with string interpolation |
| `no-runtime-exec-scala` | ASK | error | Flags `Runtime.exec()` with interpolation |
| `no-unchecked-asInstanceOf` | ASK | warning | Flags `asInstanceOf` — use pattern matching |
| `no-hardcoded-secrets-scala` | ASK | error | Flags hardcoded credentials |
| `no-scala-xml-external-entity` | DENY | error | Blocks `scala.xml.XML.load` — XXE risk |

## Compatible with

- Scala 2.13+, Scala 3.x
- Akka, Play Framework, Slick, Doobie
- Works alongside Scalafix and WartRemover

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
