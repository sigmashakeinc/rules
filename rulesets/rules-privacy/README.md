# rules-privacy

Privacy and PII governance rules for AI coding agents. Prevents logging personal data (email, phone, SSN, card numbers), PII in URL query strings, analytics without consent, and plaintext sensitive database columns — helping AI-generated code meet GDPR, CCPA, and PCI-DSS requirements.

**5 rules · 1 file**

![rules-privacy — AI agent privacy and PII governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-privacy)


## Install

```bash
ssg hub pull rules-privacy
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### privacy_write_pii.rules (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-log-pii-fields` | DENY | error | Blocks logging email/phone/SSN/card |
| `no-pii-in-url-params` | DENY | error | Blocks PII in URL query strings |
| `ask-data-retention` | LOG | info | Reminds to document retention policy |
| `no-tracking-without-consent` | ASK | warning | Flags analytics before consent check |
| `no-plaintext-sensitive-fields` | DENY | error | Blocks plaintext password/SSN DB columns |

## Compliance Coverage

- **GDPR** Articles 5, 17, 25 — privacy by design, data minimization, right to erasure
- **CCPA** — consent for tracking, right to deletion, opt-out of sale
- **PCI-DSS** — no plaintext cardholder data in logs or databases
- **HIPAA** — extend with rules-hipaa (coming soon)

## Why this matters

AI agents writing backend code frequently generate logging statements like `logger.info('User login', { email, phone })` — exposing PII in application logs that may be shipped to third-party aggregators. PII in URL parameters (e.g., `?email=user@example.com`) appears in server access logs, browser history, and referrer headers. These patterns are common in LLM-generated code and can trigger regulatory violations.

## Compatible with

- Any language with logging (TypeScript/Node.js, Python, Java, Go, Ruby)
- Any database ORM or migration tool
- Any analytics or event tracking library

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
