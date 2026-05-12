# rules-cpp

C++ security governance rules for AI coding agents. Blocks all C-level unsafe functions plus C++-specific issues: raw new/delete instead of smart pointers, reinterpret_cast bypassing type safety, C-style casts, std::system() with user input, and uncaught exception specifications.

**8 rules · 1 file**

![rules-cpp — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-cpp)

## Install

```bash
ssg hub pull rules-cpp
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### cpp_write_safety.rules — Security (8 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-gets-cpp` | DENY | error | Bans `gets()` — buffer overflow |
| `no-sprintf-cpp` | ASK | error | Flags `sprintf()` — use `snprintf()` or streams |
| `no-raw-new-delete` | ASK | warning | Flags raw `new` — use `make_unique`/`make_shared` |
| `no-reinterpret-cast` | ASK | warning | Flags `reinterpret_cast` — type safety bypass |
| `no-c-style-cast-cpp` | LOG | warning | Flags C-style casts — use C++ explicit casts |
| `no-system-cpp` | ASK | error | Flags `system()` with user input |
| `no-strcpy-cpp` | ASK | error | Flags `strcpy()`/`strcat()` — use `std::string` |
| `no-uncaught-exception-spec` | LOG | warning | Flags throws without try/catch context |

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
