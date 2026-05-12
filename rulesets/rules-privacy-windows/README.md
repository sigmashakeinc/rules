# rules-privacy-windows

Windows privacy protection governance rules for AI coding agents. Blocks reading Chrome/Edge/Firefox browsing history, Outlook PST/OST files, Windows Credential Manager, SAM/ntds.dit credential databases, Windows Timeline (ActivitiesCache.db), location data, and Recent Files activity.

**7 rules · 1 file**

![rules-privacy-windows — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-privacy-windows)

## Install

```bash
ssg hub pull rules-privacy-windows
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### windows_read_privacy.rules — Privacy (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-read-browser-history-windows` | ASK | error | Flags reading Chrome/Edge/Firefox history from AppData |
| `no-read-outlook-pst-ost` | ASK | error | Flags copying/reading Outlook PST/OST email archives |
| `no-credential-manager-read` | DENY | error | Blocks Windows Credential Manager enumeration |
| `no-read-recent-files` | ASK | warning | Flags reading Windows Recent Files and jump lists |
| `no-read-windows-activity-timeline` | ASK | warning | Flags ActivitiesCache.db (Windows Timeline) access |
| `no-windows-location-access` | ASK | error | Flags Windows location services data access |
| `no-sam-ntds-access` | DENY | error | Blocks SAM/ntds.dit credential database export |

## Compatible with

- Windows 10, 11 (all editions)
- Windows Server 2019, 2022
- Works alongside Microsoft Purview, GDPR compliance tooling, and DLP solutions

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
