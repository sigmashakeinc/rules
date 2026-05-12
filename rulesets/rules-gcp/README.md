# rules-gcp

Google Cloud Platform security governance rules for AI coding agents. Blocks hardcoded GCP service account private keys, public Cloud Storage bucket ACLs, overly permissive roles/owner and roles/editor bindings, allAuthenticatedUsers IAM grants (all 3B Google accounts), Cloud Functions with ALLOW_ALL ingress, and detects GCP API key patterns in source code.

**6 rules · 1 file**

![rules-gcp — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-gcp)

## Install

```bash
ssg hub pull rules-gcp
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### gcp_write_safety.rules — Security (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-hardcoded-gcp-service-account-key` | DENY | error | Blocks hardcoded service account private keys |
| `no-gcp-public-storage-bucket` | ASK | error | Flags public Cloud Storage bucket ACLs |
| `no-gcp-editor-owner-binding` | ASK | error | Flags roles/owner and roles/editor bindings |
| `no-gcp-all-authenticated-users` | ASK | error | Flags allAuthenticatedUsers IAM grants |
| `no-gcp-insecure-cloud-function` | ASK | error | Flags Cloud Functions with ALLOW_ALL ingress |
| `no-hardcoded-gcp-api-key` | ASK | error | Detects GCP API key pattern (AIza...) in source |

## Compatible with

- Terraform google provider, Config Connector, Deployment Manager
- gcloud CLI, Pulumi GCP
- Works alongside tfsec, Checkov, and GCP Security Command Center

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
