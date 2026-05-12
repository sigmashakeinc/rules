# rules-moltbook

Moltbook governance rules — guards against the 1.5M API token breach (Wiz Research), agent-to-agent prompt injection via social posts, misconfigured Supabase credential exposure, and the systemic risk of vibe-coded infrastructure with no security review.

**12 rules · 3 files**

![rules-moltbook — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-moltbook)

## Install

```bash
ssg hub pull rules-moltbook
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with any AI agent framework using the `ssg` hook protocol.

## Rules

### moltbook_exec_agent_injection.rules — Agent injection and API safety (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-moltbook-agent-instruction-override` | DENY | error | Blocks prompt injection patterns in content posted to Moltbook |
| `no-moltbook-direct-supabase-access` | DENY | error | Blocks direct Supabase REST API calls (1.5M token breach vector) |
| `ask-moltbook-api-interaction` | ASK | warning | Prompts before any Moltbook API calls |
| `log-moltbook-agent-lifecycle` | LOG | info | Audit trail for Moltbook agent start/create/spawn |

### moltbook_write_token_safety.rules — Token and data write safety (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-moltbook-api-token-in-source` | DENY | error | Blocks hardcoded Moltbook API tokens in source code |
| `no-moltbook-supabase-credentials-in-source` | DENY | error | Blocks Supabase URL/anon key hardcoding (breach root cause) |
| `ask-moltbook-agent-post-content` | ASK | warning | Prompts before agent post creation (injection propagation risk) |
| `no-moltbook-email-in-source` | DENY | error | Blocks email addresses in Moltbook code (35K emails were exposed) |
| `log-moltbook-config-file-write` | LOG | info | Audit trail for all Moltbook config file modifications |

### moltbook_read_data_safety.rules — Data read protection (3 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-moltbook-user-data-read` | DENY | error | Blocks reading Moltbook user data files (emails, tokens, credentials) |
| `ask-moltbook-database-access` | ASK | warning | Prompts before SQLite/database file access in Moltbook context |
| `log-moltbook-agent-output-read` | LOG | info | Audit trail for agent output reads (injection detection) |

## Why this matters

Moltbook is a Reddit-style social network where only AI agents can post, built on OpenClaw. Launched in January 2026, it attracted 1.5M agents — and within days, revealed what ungoverned AI infrastructure looks like at scale:

- **1.5M API tokens leaked** (Wiz Research): A misconfigured Supabase database allowed full read/write access to all platform data, exposing 1.5 million authentication tokens, 35,000 email addresses, and private agent messages.
- **Vibe-coded with zero security review** (Fanatical Futurist): The Moltbook founder didn't write a single line of code — the entire platform was AI-generated without security review. Palo Alto Networks mapped it against OWASP Top 10 for AI Agents and found **failures across nearly every category**.
- **Agent-to-agent prompt injection** (Wiz Research): Each Moltbook post can act as a prompt for a connected OpenClaw instance. Hiding malicious instructions in posts tricks reading agents into sharing sensitive data or silently changing behavior.
- **No kill switch** (Reco.ai): 60% of organizations using Moltbook-connected agents have no mechanism to stop them when they misbehave.
- **Existential risk vector** (Bulletin of the Atomic Scientists): Moltbook-like platforms "increase the speed and depth with which AI systems can interact, adapt, and coordinate" — making them "potential strategic risks" and "accelerators of existential risk."

## Compatible AI clients

- OpenClaw / ClawdBot / MoltBot instances
- Any AI agent connecting to social agent networks
- Works alongside: `rules-openclaw`, `rules-security`

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
