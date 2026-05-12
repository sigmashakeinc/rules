# Claude 4.6 Governance Ruleset

Protects against agentic vulnerabilities in Claude 4.6 workflows, including the Confused Deputy problem in Sonnet, the "Opus Tax" inefficiencies, and context pollution.

## Features
- **Prevents Approval Fatigue:** Stops Sonnet from executing unchecked dangerous commands.
- **Blocks Context Pollution Loops:** Restricts the execution of recursive outputs.

## Installation

```bash
ssg hub pull rules-claude-4.6
```