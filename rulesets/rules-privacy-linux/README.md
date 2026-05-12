# rules-privacy-linux

Linux privacy protection governance rules for AI coding agents. Blocks reading browser history databases, /proc/<pid>/environ (process credentials), SSH private keys, GNOME keyring secrets, user mail, shell history, and user activity logs without explicit authorization.

**7 rules · 1 file**

![rules-privacy-linux — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-privacy-linux)

## Install

```bash
ssg hub pull rules-privacy-linux
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### linux_read_privacy.rules — Privacy (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-read-browser-history-linux` | ASK | error | Flags reading Firefox/Chrome SQLite history databases |
| `no-read-proc-environ` | DENY | error | Blocks reading /proc/<pid>/environ (process credentials) |
| `no-read-user-ssh-keys` | ASK | error | Flags reading SSH private key files |
| `no-gnome-keyring-dump` | ASK | error | Flags GNOME keyring and libsecret access |
| `no-read-user-activity-logs` | ASK | warning | Flags reading wtmp/lastlog/journald user activity |
| `no-read-user-mail` | ASK | error | Flags reading /var/mail or mbox email files |
| `no-read-shell-history` | ASK | warning | Flags reading .bash_history / .zsh_history |

## Compatible with

- Ubuntu, Debian, Fedora, Arch Linux, and any systemd-based distribution
- Works alongside auditd, osquery, and GDPR compliance tooling

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
