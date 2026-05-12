# rules-testing

Test suite governance rules for AI coding agents. Blocks `.only()` focused tests that silently skip the entire suite, accumulated `.skip()` debt, hardcoded `sleep()` delays, and assertion-free tests — preventing AI-generated test code from degrading CI reliability.

**5 rules · 1 file**

![rules-testing — AI agent test suite governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-testing)


## Install

```bash
ssg hub pull rules-testing
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### test_write_hygiene.rules (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-test-only` | DENY | error | Blocks `.only()` — silently skips all other tests |
| `no-skipped-tests` | ASK | warning | Warns on `.skip()` — accumulated technical debt |
| `no-hardcoded-sleep` | DENY | error | Blocks `sleep(1000)` — use waitFor() instead |
| `no-console-in-tests` | LOG | info | Flags console.log in test files |
| `ask-no-assertions` | ASK | warning | Flags tests with no expect/assert calls |

## Why this matters

AI agents writing tests commonly produce `.only()` blocks — a debugging pattern that silently skips every other test in CI, giving false confidence. `sleep(1000)` hardcoded delays create flaky tests that fail on slow CI runners. Tests with no `expect()` calls pass unconditionally, becoming false-green checkmarks that provide zero coverage signal.

These rules catch the most common AI-generated test anti-patterns before they reach version control and corrupt your CI pipeline.

## Compatible test frameworks

- **JavaScript/TypeScript**: Jest, Vitest, Bun test, Mocha, Jasmine
- **Python**: pytest, unittest
- **Go**: testing package
- **Java**: JUnit, TestNG
- **Ruby**: RSpec, Minitest

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
