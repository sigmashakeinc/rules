# rules-jenkins

Jenkins pipeline security governance rules for AI coding agents. Blocks Groovy eval()/GroovyShell execution in Jenkinsfiles, hardcoded credentials in pipeline scripts, command injection via Groovy string interpolation of params.* in sh steps, @NonCPS sandbox bypass, agent:any without restriction, and archiving sensitive credential files as artifacts.

**6 rules · 1 file**

![rules-jenkins — AI agent governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-jenkins)

## Install

```bash
ssg hub pull rules-jenkins
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com). Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, and any AI coding agent using the `ssg` hook protocol.

## Rules

### jenkins_write_safety.rules — Security (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-groovy-eval-jenkins` | DENY | error | Bans `evaluate()`/GroovyShell in pipelines |
| `no-hardcoded-credentials-jenkins` | DENY | error | Blocks hardcoded credentials in Jenkinsfiles |
| `no-sh-string-interpolation-jenkins` | ASK | error | Flags params.* interpolation in sh steps |
| `no-script-security-bypass-jenkins` | ASK | error | Flags @NonCPS sandbox bypass |
| `no-agent-any-public-jenkins` | ASK | warning | Flags unrestricted agent:any |
| `no-archive-sensitive-artifacts-jenkins` | ASK | warning | Flags archiving .env/credential files |

## Compatible with

- Jenkins 2.x with Pipeline plugin
- Declarative and Scripted pipelines
- Works alongside Jenkins OWASP Dependency Check and Warnings NG plugin

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
