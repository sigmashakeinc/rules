# rules-swift

Swift/iOS security governance rules for AI coding agents. Catches force unwrapping crashes, disabled SSL certificate validation, SQL string interpolation, hardcoded API keys and secrets, logging sensitive data via NSLog/print, and insecure credential storage in UserDefaults (should use Keychain).

**7 rules · 1 file**

![rules-swift — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-swift)

## Install

```bash
ssg hub pull rules-swift
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### swift_write_safety.rules — Security (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-force-unwrap` | ASK | warning | Flags `!` force unwrapping — use `if let`/`guard let` |
| `no-try-force` | ASK | warning | Flags `try!` — use `do/try/catch` |
| `no-allow-invalid-ssl` | DENY | error | Blocks disabled SSL cert validation |
| `no-sql-interpolation-swift` | DENY | error | Blocks SQL string interpolation |
| `no-hardcoded-secrets-swift` | ASK | error | Flags hardcoded API keys — use Keychain |
| `no-nslog-sensitive-data` | ASK | warning | Flags logging passwords/tokens |
| `no-insecure-data-storage` | ASK | warning | Flags credentials in UserDefaults |

## Compatible with

- Swift 5.5+, iOS 14+, macOS 12+
- UIKit, SwiftUI
- Works alongside SwiftLint

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
