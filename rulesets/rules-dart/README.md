# rules-dart

Dart/Flutter security governance rules for AI coding agents. Catches null assertion crashes, dart:mirrors unavailability in Flutter production builds, command injection in Process.run, SQL injection via rawQuery interpolation, hardcoded API keys in app binaries, cleartext HTTP, and insecure credential storage in SharedPreferences (should use flutter_secure_storage).

**7 rules · 1 file**

![rules-dart — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-dart)

## Install

```bash
ssg hub pull rules-dart
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### dart_write_safety.rules — Security (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-force-unwrap-dart` | ASK | warning | Flags `!` null assertion — use `?.` or `??` |
| `no-dart-mirrors` | ASK | error | Blocks `dart:mirrors` — unavailable in Flutter |
| `no-process-run-shell-dart` | ASK | error | Flags `Process.run('sh', ...)` — command injection |
| `no-sql-interpolation-dart` | DENY | error | Blocks SQL rawQuery with interpolation |
| `no-hardcoded-secrets-dart` | ASK | error | Flags hardcoded API keys — use --dart-define |
| `no-cleartext-http-dart` | ASK | error | Flags http:// URLs in production |
| `no-insecure-shared-prefs` | ASK | warning | Flags credentials in SharedPreferences |

## Compatible with

- Dart 3.x, Flutter 3.x
- sqflite, Dio, http
- Works alongside dart analyze and flutter_lints

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
