# rules-typescript

TypeScript governance rules for AI coding agents. Enforces type safety, prevents SQL injection and XSS vulnerabilities, bans `@ts-ignore` and `any` types, and guides toward idiomatic TypeScript — catching common LLM-generated anti-patterns at the tool-call boundary.

**13 rules · 3 files**

![rules-typescript — AI agent TypeScript governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-typescript)


## Install

```bash
ssg hub pull rules-typescript
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### ts_write_safety.rules — Security & type safety (7 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `ban-ts-ignore` | DENY | error | Bans `@ts-ignore` and `@ts-nocheck` — fix the type error instead |
| `no-any-type` | DENY | error | Bans `: any`, `as any`, `<any>` — use concrete types |
| `no-eval` | DENY | error | Bans `eval()` and `new Function()` — code injection risk |
| `no-sql-interpolation` | DENY | error | Blocks template literals in `.query`/`.prepare` — SQL injection |
| `ask-inner-html` | ASK | warning | Flags `innerHTML` and `dangerouslySetInnerHTML` — XSS risk |
| `catch-unknown-not-any` | DENY | error | Bans `catch (e: any)` — use `unknown` and narrow |
| `no-non-null-assertion` | ASK | warning | Flags `!.` non-null assertions — handle null explicitly |

### ts_write_style.rules — Code quality (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-var-declarations` | LOG | warning | Flags `var` — prefer `const` or `let` |
| `no-console-log-in-src` | ASK | warning | Flags `console.log` in `src/` — use a structured logger |
| `no-empty-catch` | ASK | warning | Flags empty catch blocks — log or rethrow |
| `prefer-const-over-let` | LOG | info | Suggests `const` where `let` is never reassigned |

### ts_write_imports.rules — Import hygiene (2 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-wildcard-imports` | LOG | warning | Flags `import * as` — use named imports |
| `no-deep-relative-imports` | LOG | info | Flags `../../../` paths — use path aliases |

## Why this matters

LLMs frequently generate TypeScript code with `as any` casts, `@ts-ignore` suppressions, and template-literal SQL queries — patterns that defeat TypeScript's type system and introduce security vulnerabilities. These rules intercept those patterns at the moment the agent writes the code, before they reach version control.

- **Type safety**: `any` types and `@ts-ignore` comments let runtime errors slip through the type checker
- **SQL injection prevention**: Template literals in `.query()` calls are a leading source of injection vulnerabilities in TypeScript backends
- **XSS protection**: `innerHTML` and `dangerouslySetInnerHTML` with unsanitized values cause cross-site scripting

## Compatible with

- TypeScript 4.x / 5.x
- Any TypeScript project (Next.js, Node.js, Bun, Deno, etc.)
- Works alongside ESLint — these rules operate at the agent tool-call level, not at build time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
