# rules-docker

Docker and Docker Compose security rules for AI coding agents. Prevents root user containers, `:latest` image tags, secrets in `ENV` layers, privileged mode, and unbound port exposure — enforcing container security best practices at the agent tool-call boundary.

**6 rules · 1 file**

![rules-docker — AI agent Docker security governance demo](demo.cast)

> [▶ Watch interactive demo on SigmaShake Hub](https://hub.sigmashake.com/ruleset/rules-docker)


## Install

```bash
ssg hub pull rules-docker
```

Available on the [SigmaShake Hub](https://hub.sigmashake.com) — the open registry for AI agent governance rules. Compatible with Claude Code, GitHub Copilot, Cursor, Windsurf, Aider, and any AI coding agent using the `ssg` hook protocol.

## Rules

### docker_write_security.rules (6 rules)

| Rule | Decision | Severity | Description |
|------|----------|----------|-------------|
| `no-run-as-root` | DENY | error | Requires non-root USER in Dockerfile |
| `no-latest-tag` | DENY | error | Bans `:latest` tag — pin exact versions |
| `no-add-for-files` | ASK | warning | Prefers COPY over ADD for local files |
| `no-secrets-in-env` | DENY | error | Blocks secrets in ENV/docker-compose |
| `no-privileged-container` | DENY | error | Blocks `privileged: true` in compose |
| `no-expose-all-ports` | ASK | warning | Warns on 0.0.0.0 port binding |

## Why this matters

AI agents writing Dockerfiles commonly produce containers that run as root (a CIS Docker Benchmark violation), use `:latest` tags (breaking reproducibility), and embed secrets in `ENV` instructions (which are visible in `docker inspect` and image layers). `privileged: true` in Docker Compose grants a container full host access — equivalent to running as root on the host machine.

These rules enforce the CIS Docker Benchmark and Docker security best practices at the moment the agent writes the Dockerfile — before the image is built or pushed to a registry.

## Compatible with

- Docker 20.x+, Docker Compose v2
- Dockerfile, docker-compose.yml, docker-compose.yaml
- Works alongside Docker Scout, Trivy, and Hadolint — these rules operate at the agent tool-call level, not at build time

## About

Part of the [SigmaShake Hub](https://hub.sigmashake.com) — open-source governance rules for AI coding agents.
Install the `ssg` CLI to enforce these rules: `npm install -g @sigmashake/ssg`
