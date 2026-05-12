# Gemini 3.1 Governance Ruleset

Designed specifically to mitigate vulnerabilities associated with the Gemini 3.1 agent tool execution model. This addresses the latest context injection methods and over-privileged execution scenarios unique to the Gemini 3.1 Pro and Flash variants.

## Features
- **Prevents Indirect Prompt Injection (IDPI):** Blocks the execution of known exploit vectors when analyzing external workspaces.
- **Mitigates Tool Hijacking:** Employs HITL when executing sensitive commands or accessing restricted scopes.

## Installation

```bash
ssg hub pull rules-gemini-3.1
```