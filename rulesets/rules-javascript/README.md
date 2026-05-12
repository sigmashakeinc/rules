# rules-javascript

JavaScript security and code quality governance rules for AI coding agents. Blocks eval()/new Function() code injection, prototype pollution via `__proto__`, command injection in child_process.exec(), SQL template literal injection, XSS via innerHTML/document.write(), path traversal in file operations, and insecure randomness for cryptographic values.

**13 rules · 2 files**

![rules-javascript — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-javascript)

## Install

```bash
ssg hub pull rules-javascript
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### js_write_safety.rules — Security (9 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-eval` | DENY | error | Bans `eval()` — arbitrary code execution |
| `no-new-function` | DENY | error | Bans `new Function()` — runtime code construction |
| `no-prototype-pollution` | DENY | error | Blocks `__proto__` mutation — prototype pollution |
| `no-child-process-exec-concat` | DENY | error | Blocks string concat/interpolation in exec() |
| `no-sql-template-literal` | DENY | error | Blocks template literals in SQL queries |
| `no-innerhtml-assignment` | ASK | error | Flags innerHTML/document.write — XSS risk |
| `no-require-user-input` | DENY | error | Blocks require() with user-supplied paths |
| `no-math-random-crypto` | DENY | error | Bans Math.random() for tokens/secrets/keys |
| `no-hardcoded-secrets-js` | ASK | error | Flags hardcoded credentials in JS files |
| `no-path-traversal-js` | ASK | error | Flags file ops with user-controlled paths |

### js_write_style.rules — Code quality (4 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-var-declaration` | LOG | warning | Flags `var` — use `const`/`let` |
| `no-empty-catch-js` | ASK | warning | Flags empty catch blocks |
| `no-console-log-in-src-js` | LOG | warning | Flags console.log() in src/ |
| `no-loose-equality` | LOG | warning | Flags `==`/`!=` — use `===`/`!==` |

## Why this matters

JavaScript's dynamic nature makes it highly susceptible to AI-generated security issues. `eval()` and `new Function()` with user-controlled strings are the textbook RCE pattern. Prototype pollution via `__proto__` can compromise all objects in the process. SQL template literals with interpolated variables bypass all ORM protections. `innerHTML` with untrusted content is the #1 XSS vector in browser applications.

## Compatible with

- Node.js 14+, Bun, Deno
- Express, Fastify, Koa, Hono
- Works alongside ESLint, Semgrep — these rules operate at the agent tool-call level

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
