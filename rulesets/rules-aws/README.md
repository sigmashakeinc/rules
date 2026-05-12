# rules-aws

AWS CLI governance rules for AI coding agents. Blocks public S3 bucket ACLs, wildcard IAM policies (`Action: "*"`), and accidental resource deletion — preventing the most costly AWS misconfigurations and data exposure incidents caused by autonomous AI agents.

**5 rules · 1 file**

![rules-aws — AI agent AWS CLI governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-aws)


## Install

```bash
ssg hub pull rules-aws
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### aws_exec_safety.rules (5 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-s3-public-acl` | DENY | error | Blocks public-read/public-read-write S3 ACLs |
| `no-iam-star-permissions` | DENY | error | Blocks IAM `Action: "*"` wildcard |
| `no-resource-star-with-write` | ASK | warning | Warns on `Resource: "*"` in IAM policies |
| `ask-aws-delete` | ASK | warning | Confirms before s3 rm, ec2 terminate, rds delete |
| `log-aws-profile` | LOG | info | Logs all AWS CLI commands with profile reminder |

## Why this matters

AI agents with AWS CLI access can expose S3 buckets to the public internet in a single command (`--acl public-read`). Wildcard IAM policies granting `Action: "*"` violate the AWS Well-Architected Framework's principle of least privilege and are a direct path to privilege escalation. Accidental `aws ec2 terminate-instances` or `aws s3 rm --recursive` can destroy production data with no undo.

These rules act as a last line of defense between an AI agent and your AWS account — blocking the most dangerous operations and requiring human confirmation for destructive ones.

## Compatible with

- AWS CLI v2
- Any automation using `aws` commands (scripts, CI/CD, agent workflows)
- Works alongside AWS Config, AWS SecurityHub, and IAM Access Analyzer — these rules operate at the agent tool-call level, before commands reach AWS

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
