# rules-react

React and JSX governance rules for AI coding agents. Prevents XSS via `dangerouslySetInnerHTML`, enforces React hooks correctness (no hooks in conditionals, no setState in render), and catches accessibility violations — blocking security and correctness issues at the agent tool-call boundary.

**13 rules · 3 files**

![rules-react — AI agent React governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-react)


## Install

```bash
ssg hub pull rules-react
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### react_write_safety.rules — XSS and security (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-dangerous-html` | DENY | error | Blocks unsanitized `dangerouslySetInnerHTML` |
| `no-href-javascript` | DENY | error | Blocks `href="javascript:"` — XSS risk |
| `ask-external-url-href` | ASK | warning | Validates dynamic href values |
| `no-target-blank-without-rel` | DENY | error | Requires `rel="noopener noreferrer"` with `target="_blank"` |
| `no-missing-key-in-list` | LOG | warning | Flags `.map()` without key props |

### react_write_hooks.rules — Hooks correctness (3 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-hooks-in-conditionals` | DENY | error | Blocks hooks inside if statements |
| `ask-empty-dep-array` | ASK | warning | Verifies empty `[]` deps are intentional |
| `no-setstate-in-render` | DENY | error | Blocks setState calls in render body |

### react_write_a11y.rules — Accessibility (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-img-without-alt` | DENY | error | img element missing alt attribute |
| `no-click-without-keyboard` | ASK | warning | onClick on non-interactive element without keyboard handler |
| `no-aria-hidden-on-focusable` | DENY | error | aria-hidden on focusable element creates keyboard trap |
| `no-empty-button-label` | DENY | error | Button with no text or aria-label |
| `no-autofocus` | LOG | warning | autoFocus disorients screen reader users |

## Why this matters

AI agents writing React components commonly produce: `dangerouslySetInnerHTML` with raw user data (XSS), hooks inside conditional branches (React invariant violation), and images without alt text (WCAG failure). These aren't caught by TypeScript — they require semantic understanding of the React component model.

- **XSS prevention**: `dangerouslySetInnerHTML` and `href="javascript:"` are the leading sources of frontend XSS
- **Hooks correctness**: Hooks inside conditionals cause the "rendered more hooks than previous render" error that breaks entire component trees
- **Accessibility compliance**: Missing alt attributes and aria-hidden on focusable elements fail WCAG 2.1 AA

## Compatible with

- React 16.8+ (hooks required for hooks rules)
- TypeScript (.tsx) and JavaScript (.jsx)
- Works alongside ESLint + eslint-plugin-jsx-a11y — these rules operate at the agent tool-call level, not at build time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
