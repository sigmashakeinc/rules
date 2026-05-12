# rules-macos

macOS security and safety governance rules for AI coding agents. Blocks disabling SIP (csrutil), Gatekeeper bypass, TCC permission reset, osascript admin escalation, NVRAM security settings, Keychain dump, firewall disable, LaunchDaemon persistence, ATS bypass (NSAllowsArbitraryLoads), and sandbox disabling.

**13 rules · 2 files**

![rules-macos — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-macos)

## Install

```bash
ssg hub pull rules-macos
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### macos_exec_safety.rules — Security (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-csrutil-disable` | DENY | error | Blocks csrutil disable (SIP bypass) |
| `no-gatekeeper-disable` | DENY | error | Blocks spctl --master-disable (Gatekeeper bypass) |
| `no-tccutil-reset` | ASK | error | Flags full TCC privacy permission reset |
| `no-osascript-admin-privileges` | ASK | error | Flags osascript do shell script with admin privesc |
| `no-nvram-security-clear` | ASK | error | Flags NVRAM clear and insecure boot-args |
| `no-launchctl-unload-security-daemon` | ASK | error | Flags unloading trustd/syspolicyd security daemons |
| `no-keychain-export-all` | ASK | error | Flags full keychain export and password extraction |
| `no-disable-firewall-macos` | ASK | error | Flags disabling macOS application firewall or pf |

### macos_write_safety.rules — Security (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-launchagent-all-users` | ASK | error | Flags system-wide LaunchAgent/Daemon persistence |
| `no-plist-allow-arbitrary-loads` | DENY | error | Blocks NSAllowsArbitraryLoads ATS bypass |
| `no-com-apple-security-disabled` | DENY | error | Blocks sandbox disable and get-task-allow in prod |
| `no-plist-world-writable` | ASK | error | Flags world-writable plists and /tmp scripts |
| `no-hosts-file-macos` | ASK | warning | Flags redirecting Apple/iCloud domains in /etc/hosts |

## Compatible with

- macOS 12 Monterey, 13 Ventura, 14 Sonoma, 15 Sequoia
- Works alongside Santa, Jamf Pro, Munki, and CIS macOS Benchmark

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
