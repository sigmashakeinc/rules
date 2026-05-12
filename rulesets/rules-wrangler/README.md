# rules-wrangler

Cloudflare Wrangler governance rules for AI coding agents. Protects against destructive remote-database operations, secrets leakage in `wrangler.toml`, missing compatibility dates, public bucket misconfiguration, and production deploys without environment gates — at the moment the agent writes config or runs the CLI.

**25 rules · 3 files**

> [▶ View on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-wrangler)

## Install

```bash
ssg hub pull rules-wrangler
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### wrangler_write_config.rules — wrangler.toml safety (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `wrangler-secret-in-vars` | DENY | error | Blocks API keys / tokens / passwords in `[vars]` — use `wrangler secret put` |
| `wrangler-missing-compat-date` | DENY | error | Requires `compatibility_date` — undefined runtime otherwise |
| `wrangler-stale-compat-date` | LOG | warning | Flags compat dates older than 2023 |
| `wrangler-public-r2-bucket` | DENY | error | Blocks `public_bucket = true` — world-readable r2.dev URLs |
| `wrangler-wildcard-route` | DENY | error | Blocks bare `*` routes — hijacks all account traffic |
| `wrangler-node-compat-deprecated` | LOG | warning | Flags removed `node_compat = true` — use `nodejs_compat` flag |
| `wrangler-usage-model-removed` | LOG | warning | Flags ignored `usage_model` field |
| `wrangler-main-missing` | LOG | warning | Requires explicit `main` entry point |

### wrangler_bash_safety.rules — CLI command safety (10 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `wrangler-d1-remote-destructive` | DENY | error | Blocks DROP/TRUNCATE/unbounded DELETE against `--remote` D1 |
| `wrangler-d1-execute-no-dry-run` | ASK | warning | Warns on `--remote` execute without `--dry-run` |
| `wrangler-d1-migrations-apply-prod` | ASK | warning | Confirms before applying migrations to production D1 |
| `wrangler-kv-bulk-delete` | DENY | error | Blocks bulk KV deletes on remote namespaces |
| `wrangler-r2-bucket-delete` | DENY | error | Blocks `r2 bucket delete` — unrecoverable |
| `wrangler-deploy-no-env` | ASK | warning | Warns on `wrangler deploy` without `--env` flag |
| `wrangler-login-in-ci` | LOG | warning | Flags interactive `wrangler login` in CI workflows |
| `wrangler-tail-prod` | LOG | info | Flags `tail` on production — PII exposure risk |
| `wrangler-secret-put-inline` | DENY | error | Blocks `echo secret \| wrangler secret put` — shell-history leak |
| `wrangler-local-persist-gitignore` | LOG | info | Reminds to gitignore `.wrangler/` persistence dir |

### wrangler_write_workers.rules — Worker runtime safety (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `worker-fetch-unbounded-subrequest` | LOG | warning | Flags loops with `await fetch()` — 50/1000 subrequest limit |
| `worker-env-log` | DENY | error | Blocks `console.log(env)` — leaks every bound secret |
| `worker-crypto-weak-random` | DENY | error | Blocks `Math.random()` for tokens/secrets — use Web Crypto |
| `worker-durable-object-no-blockconcurrency` | LOG | info | Recommends `blockConcurrencyWhile` for DO state init |
| `worker-cache-personalized-response` | ASK | warning | Flags caching Authorization/Cookie responses — cross-user leak |
| `worker-fetch-no-timeout` | LOG | info | Suggests `AbortSignal.timeout()` on fetch calls |
| `worker-d1-string-concat-query` | DENY | error | Blocks SQL injection via template literals / `+` in `.prepare()` |

## Why this matters

Cloudflare Workers failures tend to be silent and production-scoped: a `wrangler deploy` without `--env` clobbers production, `public_bucket = true` leaks every object written since, a secret in `[vars]` gets committed and never rotated. Wrangler's CLI defaults favor velocity, so the guardrails have to move to the agent.

These rules intercept:
- **Data destruction**: `DROP`/`TRUNCATE`/unbounded `DELETE` against `--remote` D1, KV bulk deletes, R2 bucket deletes.
- **Secret leakage**: secrets in `wrangler.toml` committed to git, `console.log(env)` exposing bindings, `echo secret | wrangler secret put` leaving shell history.
- **Misconfiguration**: missing `compatibility_date`, wildcard routes, deprecated `node_compat`, public R2 buckets.
- **Worker runtime bugs**: SQL injection in D1 queries, `Math.random()` used for tokens, unbounded subrequest loops, un-keyed caching of personalized responses.

## Compatible with

- Wrangler v3.x / v4.x
- Cloudflare Workers (ESM and Service Worker formats)
- D1, KV, R2, Durable Objects, Queues

## License

MIT
