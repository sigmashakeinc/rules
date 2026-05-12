# rules-windows

Windows security and safety governance rules for AI coding agents. Blocks PowerShell execution policy bypass, encoded commands, Run key registry persistence, Windows Defender disable, SYSTEM scheduled tasks, user account creation, WMI process execution, Everyone:F permissions, autorun.inf creation, startup folder persistence, and SAM/SECURITY registry export.

**13 rules · 2 files**

![rules-windows — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-windows)

## Install

```bash
ssg hub pull rules-windows
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### windows_exec_safety.rules — Security (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-powershell-execution-bypass` | DENY | error | Blocks PowerShell -ExecutionPolicy Bypass |
| `no-powershell-encoded-command` | ASK | error | Flags -EncodedCommand obfuscated PowerShell |
| `no-reg-add-run-keys` | ASK | error | Flags Run/RunOnce registry persistence |
| `no-disable-windows-defender` | DENY | error | Blocks disabling Defender real-time monitoring |
| `no-schtasks-system-account` | ASK | error | Flags SYSTEM-level scheduled task creation |
| `no-net-user-add` | ASK | error | Flags local user creation and admin group add |
| `no-wmic-process-execution` | ASK | error | Flags WMI process call create |
| `no-icacls-everyone-full` | DENY | error | Blocks granting Everyone:F (full control) |

### windows_write_safety.rules — Security (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-hosts-file-redirect` | ASK | error | Flags redirecting Microsoft/Windows Update domains |
| `no-autorun-inf` | DENY | error | Blocks creation of autorun.inf files |
| `no-startup-folder-write` | ASK | error | Flags writes to Windows Startup persistence folders |
| `no-defender-exclusion` | ASK | error | Flags Add-MpPreference exclusion paths |
| `no-reg-export-sensitive` | ASK | error | Flags SAM/SECURITY/LSA registry hive exports |

## Compatible with

- Windows 10, 11 (all editions)
- Windows Server 2019, 2022
- Works alongside Microsoft Defender for Endpoint, CIS Windows Benchmark, LGPO

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
