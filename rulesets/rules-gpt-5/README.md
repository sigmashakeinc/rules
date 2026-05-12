# GPT-5 Governance Ruleset

This ruleset provides governance and guardrails for GPT-5 class agentic systems. With increased agency and reasoning, GPT-5 models are susceptible to Indirect Prompt Injection (IPI) via web search and un-sandboxed execution.

## Features
- **Blocks Unsandboxed Execution:** Prevents python_repl or shell environments from accessing host paths natively.
- **Human-in-the-Loop for IPI Risks:** Demands approval before passing raw, untrusted web fetch outputs back into the context.

## Installation

```bash
ssg hub pull rules-gpt-5
```