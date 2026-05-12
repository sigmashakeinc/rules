# rules-llm

LLM and AI API governance rules for AI coding agents. Prevents API key exposure in source code (`sk-...`, `ant-...`), prompt injection via system prompts, runaway inference costs from uncapped `max_tokens`, PII leakage in LLM response logs, and unsafe `temperature` settings in production AI applications.

**6 rules · 1 file**

![rules-llm — AI agent LLM API governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-llm)


## Install

```bash
ssg hub pull rules-llm
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### llm_write_safety.rules (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-hardcoded-api-key` | DENY | error | Blocks `sk-...`, `ant-...` keys in source |
| `no-unpinned-model-version` | LOG | warning | Warns on model aliases like `gpt-4` without date pin |
| `ask-max-tokens-missing` | LOG | warning | Reminds to set max_tokens on API calls |
| `no-user-input-in-system-prompt` | ASK | warning | Prevents prompt injection via system prompt |
| `no-logging-llm-responses` | ASK | warning | Guards against PII in LLM response logs |
| `ask-temperature-above-one` | LOG | warning | Flags temperature > 1.0 as non-production |

## Why this matters

AI agents building AI-powered applications produce a specific class of LLM security vulnerabilities: hardcoded OpenAI or Anthropic API keys that get committed to version control, system prompts that concatenate user input (enabling prompt injection), and LLM response logging that captures PII from model outputs.

These rules govern the application layer of AI development — helping agents write safe, cost-controlled, prompt-injection-resistant LLM integrations.

## Compatible AI clients and SDKs

- OpenAI API / ChatGPT / GPT-4
- Anthropic API / Claude / Claude Code
- Google Gemini API / Gemini CLI
- GitHub Copilot API
- Codex CLI
- LangChain, LlamaIndex, LangGraph, CrewAI
- Any custom LLM integration

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
