# rules-privacy-macos

macOS privacy protection governance rules for AI coding agents. Blocks direct database access to Contacts (AddressBook.sqlitedb), Messages (chat.db), Photos library, Safari history, CoreLocation cache, HealthKit (HIPAA-protected), and Keychain. Flags automated screen capture.

**8 rules · 1 file**

![rules-privacy-macos — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-privacy-macos)

## Install

```bash
ssg hub pull rules-privacy-macos
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### macos_read_privacy.rules — Privacy (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-read-contacts-db` | DENY | error | Blocks direct AddressBook.sqlitedb access |
| `no-read-messages-db` | DENY | error | Blocks direct Messages chat.db access |
| `no-read-photos-library` | ASK | error | Flags Photos.photoslibrary direct access |
| `no-read-safari-history` | ASK | error | Flags Safari History.db and Bookmarks.db access |
| `no-screencapture-automated` | ASK | error | Flags silent screencapture without UI sound |
| `no-read-location-data` | ASK | error | Flags CoreLocation cache and routined.db access |
| `no-read-health-data` | DENY | error | Blocks HealthKit database access (HIPAA-sensitive) |
| `no-read-keychain-db-macos` | DENY | error | Blocks raw Keychain database file access |

## Compatible with

- macOS 12 Monterey through 15 Sequoia
- Enforces the intent of TCC (Transparency, Consent, and Control) framework
- Works alongside GDPR, HIPAA, and CCPA compliance tooling

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
