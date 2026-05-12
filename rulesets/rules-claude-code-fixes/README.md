# Claude Code Fixes & Pain Point Resolutions

Are you experiencing the **"Claude Code infinite loop"**, high **token spend**, or did Claude Code **accidentally delete your code**? You are not alone. These are the most common complaints on Reddit, X, and GitHub for Anthropic's Claude Code CLI as of early 2026.

This SigmaShake ruleset acts as a permanent guardrail to fix these exact pain points, saving you API costs and protecting your codebase from autonomous mistakes.

## Solved Reddit Complaints
- **"Claude Code deleted my uncommitted work!"** -> We block `git reset --hard`, `git checkout .`, and `git clean -fd` so the agent can't "rage-quit" and wipe your local changes when a task gets difficult.
- **"Claude Code cost is too high / token burn!"** -> We block the agent from executing massive reads like `cat package-lock.json` or running runaway `find` commands that blow up your context window and drain your API credits (the "Startup Tax" and context bloat issues).
- **"Claude Code forgot my instructions!"** -> We strictly `DENY` the agent from modifying or overwriting your `CLAUDE.md` file, ensuring its project context and safety rules remain intact and aren't "compacted" away.
- **"Silent Fake Success" & Test Rigging** -> We intercept attempts by the agent to silently override unit tests or insert empty try/catch blocks to fake a successful feature implementation.

## Installation

```bash
ssg hub pull rules-claude-code-fixes
```