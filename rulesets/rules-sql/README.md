# rules-sql

SQL and database safety rules for AI coding agents. Blocks accidental data loss from `DELETE` without `WHERE`, `UPDATE` without `WHERE`, and unconfirmed `TRUNCATE` or `DROP TABLE` — preventing irreversible database operations before they execute.

**5 rules · 1 file**

![rules-sql — AI agent SQL database safety governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-sql)


## Install

```bash
ssg hub pull rules-sql
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### sql_write_safety.rules (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-drop-table-without-confirm` | DENY | error | Requires `IF EXISTS` on DROP TABLE |
| `ask-truncate` | ASK | error | Confirms before TRUNCATE TABLE |
| `no-delete-without-where` | DENY | error | Blocks DELETE without WHERE clause |
| `no-update-without-where` | DENY | error | Blocks UPDATE without WHERE clause |
| `ask-alter-column-drop` | ASK | warning | Confirms before DROP COLUMN |

## Why this matters

`DELETE FROM users` and `UPDATE orders SET status = 'shipped'` (both without `WHERE`) are among the most catastrophic SQL mistakes — they affect every row in the table and cannot be undone without a backup restore. AI agents writing database migration scripts or ad-hoc queries can produce these patterns when synthesizing SQL from natural language.

These rules block the most destructive SQL patterns at the tool-call boundary — before the query reaches a database connection.

## Compatible with

- PostgreSQL, MySQL, SQLite, SQL Server, Oracle
- Any ORM or query builder that generates raw SQL
- Works alongside migration frameworks (Flyway, Liquibase, Alembic) — these rules operate at the agent tool-call level, not at query time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
