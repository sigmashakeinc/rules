# rules-azure

Microsoft Azure infrastructure security governance rules for AI coding agents. Blocks hardcoded Azure Storage connection strings and account keys, public blob container access, over-permissive Owner/Contributor IAM assignments, disabled HTTPS-only enforcement, and unnecessary public network access on databases and key vaults.

**6 rules · 1 file**

![rules-azure — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-azure)

## Install

```bash
ssg hub pull rules-azure
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### azure_write_safety.rules — Security (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-hardcoded-azure-connection-string` | DENY | error | Blocks hardcoded Azure connection strings |
| `no-hardcoded-azure-storage-key` | DENY | error | Blocks hardcoded storage account keys |
| `no-azure-public-blob-container` | ASK | error | Flags public blob container access |
| `no-azure-overly-permissive-role` | ASK | error | Flags Owner/Contributor role assignments |
| `no-azure-disabled-https` | DENY | error | Blocks disabled HTTPS-only enforcement |
| `no-azure-public-network-access` | ASK | warning | Flags public network access on resources |

## Compatible with

- Terraform azurerm provider, Bicep, ARM templates
- Azure CLI, Pulumi Azure Native
- Works alongside tfsec, Checkov, and Azure Policy

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
