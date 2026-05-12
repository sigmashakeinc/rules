# rules-php

PHP security governance rules for AI coding agents. Blocks eval() code injection, command injection via system()/exec()/passthru(), SQL injection via string concatenation, remote/local file inclusion, XSS via unescaped echo, object injection via unserialize(), and SSRF via file_get_contents with user-controlled URLs.

**9 rules · 1 file**

![rules-php — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-php)

## Install

```bash
ssg hub pull rules-php
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### php_write_safety.rules — Security (9 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-eval-php` | DENY | error | Bans `eval()` — arbitrary code execution |
| `no-command-injection-php` | DENY | error | Blocks system()/exec()/passthru() with variables |
| `no-sql-injection-php` | DENY | error | Blocks SQL string concatenation |
| `no-dynamic-file-inclusion` | DENY | error | Blocks include/require with variable paths |
| `no-echo-unescaped-input` | ASK | error | Flags unescaped $_GET/$_POST in echo |
| `no-unserialize-user-input` | DENY | error | Blocks unserialize() with user input |
| `no-ssrf-php` | ASK | error | Flags file_get_contents/curl with user URLs |
| `no-hardcoded-secrets-php` | ASK | error | Flags hardcoded credentials |
| `no-disabled-error-reporting` | LOG | warning | Flags error_reporting(0) in production |

## Compatible with

- PHP 7.4+, PHP 8.x
- Laravel, Symfony, WordPress, CodeIgniter
- Works alongside PHPStan, PHPCS

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
