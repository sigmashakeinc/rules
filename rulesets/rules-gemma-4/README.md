# Gemma 4 Governance Ruleset

Protects against architectural footguns introduced by Gemma 4's massive 256K context window and native function calling. Gemma 4 is highly susceptible to REPL-based sandbox escapes and multimodal exfiltration.

## Features
- **Prevents REPL Escapes:** Blocks unsandboxed Python execution.
- **Mitigates Recursive Loop Exhaustion:** Enforces limits on runaway tool chains.

## Installation

```bash
ssg hub pull rules-gemma-4
```