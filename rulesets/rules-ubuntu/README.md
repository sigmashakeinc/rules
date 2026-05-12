# rules-ubuntu

Ubuntu/Linux security and safety governance rules for AI coding agents. Blocks disabling AppArmor/SELinux/UFW, NOPASSWD sudoers, SUID/SGID bit setting, direct /etc/shadow access, SSH root login and password auth, world-writable cron jobs, and pam_permit.so misuse.

**13 rules · 2 files**

![rules-ubuntu — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-ubuntu)

## Install

```bash
ssg hub pull rules-ubuntu
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### ubuntu_exec_safety.rules — Security (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-visudo-bypass` | DENY | error | Blocks direct /etc/sudoers edits — use visudo |
| `no-nopasswd-sudo` | ASK | error | Flags NOPASSWD in sudo commands |
| `no-disable-apparmor` | DENY | error | Blocks disabling AppArmor mandatory access control |
| `no-disable-ufw` | ASK | error | Flags UFW/iptables flush/disable |
| `no-suid-setgid` | ASK | error | Flags chmod +s / SUID/SGID bit setting |
| `no-selinux-disable` | DENY | error | Blocks setenforce 0 and SELINUX=disabled |
| `no-read-etc-shadow` | DENY | error | Blocks direct reads of /etc/shadow |
| `no-passwd-root-direct` | ASK | error | Flags direct root password changes |

### ubuntu_write_safety.rules — Security (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-ssh-permitrootlogin` | DENY | error | Blocks PermitRootLogin yes in sshd_config |
| `no-ssh-passwordauth` | ASK | error | Flags PasswordAuthentication yes in sshd_config |
| `no-sudoers-nopasswd` | ASK | error | Flags NOPASSWD in sudoers/sudoers.d files |
| `no-world-writable-cron` | DENY | error | Blocks world-writable cron job files |
| `no-pam-permissive` | ASK | error | Flags pam_permit.so bypassing authentication |

## Compatible with

- Ubuntu 20.04, 22.04, 24.04 LTS
- Debian 11/12, Pop!_OS, Linux Mint
- Works alongside Lynis, OpenSCAP, CIS Benchmark audits

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
