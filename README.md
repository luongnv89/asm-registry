# asm-registry

Curated registry of agent skills for [Agent Skill Manager (asm)](https://github.com/luongnv89/agent-skill-manager).

## What is this?

This repository serves as the central registry for discovering and installing agent skills via `asm install <skill-name>`. Each skill is represented by a JSON manifest that points to its source repository and commit.

## Structure

```
schema/
  manifest.v1.json       # JSON Schema for manifest validation
manifests/
  <author>/
    <skill-name>.json    # One manifest per skill
index.json               # Auto-generated index of all skills
```

## Installing skills from the registry

```bash
# Install by bare name
asm install code-review

# Install by scoped name
asm install luongnv89/skill-auditor
```

## Publishing a skill

```bash
# From your skill repository
asm publish
```

Or submit manually — see [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

## Manifest schema

Each manifest follows `schema/manifest.v1.json`. Key fields:

| Field | Description |
|-------|-------------|
| `name` | Lowercase skill name (`[a-z0-9-]`) |
| `author` | GitHub username of the publisher |
| `repository` | Source repo URL |
| `commit` | Pinned commit SHA (40 hex chars) |
| `version` | Semantic version |
| `description` | One-line description |
| `tags` | Categorization tags |
| `security_verdict` | Result of security audit |

## CI Pipeline

- **validate-pr.yml** — Runs on every PR: schema validation, author identity check, duplicate detection, typosquat detection, and independent security scan.
- **rebuild-index.yml** — Runs on merge to main: rebuilds `index.json` from all manifests.

## License

MIT
