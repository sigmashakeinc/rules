# rules-csharp

C# security governance rules for AI coding agents. Blocks SQL string concatenation, BinaryFormatter deserialization (deprecated RCE vector), XML external entity injection, command injection via Process.Start, path traversal, LDAP injection, hardcoded connection strings, and broken cryptography (MD5/SHA-1).

**8 rules · 1 file**

![rules-csharp — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-csharp)

## Install

```bash
ssg hub pull rules-csharp
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### cs_write_safety.rules — Security (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-sql-string-concat-cs` | DENY | error | Blocks SQL string concatenation — use SqlParameter |
| `no-binary-formatter` | DENY | error | Bans BinaryFormatter/SoapFormatter — deprecated RCE |
| `no-xml-external-entity-cs` | DENY | error | Requires disabled DTD processing — prevents XXE |
| `no-process-start-shell-cs` | ASK | error | Flags Process.Start with shell execution |
| `no-hardcoded-connection-string` | ASK | error | Flags hardcoded connection strings |
| `no-ldap-injection-cs` | DENY | error | Blocks string concat/interpolation in LDAP filters |
| `no-md5-sha1-cs` | ASK | error | Flags MD5/SHA-1 usage — use SHA-256 or BCrypt |
| `no-path-traversal-cs` | ASK | error | Flags file ops with user-controlled paths |

## Compatible with

- .NET 6+, .NET Framework 4.8+
- ASP.NET Core, Entity Framework
- Works alongside Roslyn analyzers and Security Code Scan

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
