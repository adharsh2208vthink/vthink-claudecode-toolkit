# Toolkit Catalog

This file is the **single source of truth** for everything in the toolkit. When you add a new skill, agent, command, or hook, **update this file as part of your PR**.

> Keep entries sorted alphabetically within each section.

---

## Agents

Sub-agents with defined roles and responsibilities. Place files in `agents/<category>/`.

### core-development

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

### code-review

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

### testing

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

### devops

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

---

## Skills

Workflow and domain knowledge prompts. Place files in `skills/<category>/`.

### frontend

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

### backend

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

### data

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

---

## Slash Commands

Invocable via `/command-name` in Claude Code. Place files in `.claude/commands/`.

| Name | Invocation | File | Description | Author |
|------|-----------|------|-------------|--------|
| _(none yet)_ | | | | |

---

## Hooks

Shell scripts triggered by Claude Code tool events. Place in `hooks/pre-tool/` or `hooks/post-tool/`.

### pre-tool

| Name | File | Trigger | Description | Author |
|------|------|---------|-------------|--------|
| _(none yet)_ | | | | |

### post-tool

| Name | File | Trigger | Description | Author |
|------|------|---------|-------------|--------|
| _(none yet)_ | | | | |

---

## Rules

CLAUDE.md snippets for always-follow instructions. Place files in `rules/`.

| Name | File | Description | Author |
|------|------|-------------|--------|
| _(none yet)_ | | | |

---

## MCP Configurations

Ready-to-paste MCP server config snippets. Place files in `mcp/`.

| Name | File | What it enables | Notes |
|------|------|-----------------|-------|
| filesystem | [`mcp/filesystem.json`](mcp/filesystem.json) | Scoped file access outside the project directory | Set allowed paths |
| github | [`mcp/github.json`](mcp/github.json) | Read/write GitHub issues, PRs, repos | Requires `$GITHUB_TOKEN` |
| postgres | [`mcp/postgres.json`](mcp/postgres.json) | Query a PostgreSQL database | Requires `$PG_CONNECTION_STRING` |
| puppeteer | [`mcp/puppeteer.json`](mcp/puppeteer.json) | Browser automation and web scraping | Downloads Chromium on first use |
| sqlite | [`mcp/sqlite.json`](mcp/sqlite.json) | Query a local SQLite database | Set db file path |

---

## Settings Templates

Pre-built `.claude/settings.json` starters by project type. Place files in `settings-templates/`.

| Name | File | For |
|------|------|-----|
| java-spring | [`settings-templates/java-spring.json`](settings-templates/java-spring.json) | Java / Spring Boot (Maven) |
| nodejs | [`settings-templates/nodejs.json`](settings-templates/nodejs.json) | Node.js / Express backend |
| python | [`settings-templates/python.json`](settings-templates/python.json) | Python (pip / poetry / uv) |
| react | [`settings-templates/react.json`](settings-templates/react.json) | React frontend (CRA / Vite / Next.js) |

---

## Workflows

Multi-agent orchestration patterns. Place files in `workflows/`.

| Name | File | Description | Author |
|------|------|-------------|--------|
| feature-development | [`workflows/feature-development.md`](workflows/feature-development.md) | BDD → implement → test → ship. Full cycle from feature description to pushed code. | adharsh2208vthink |
| pr-review-pipeline | [`workflows/pr-review-pipeline.md`](workflows/pr-review-pipeline.md) | Conventions check → test runner → QA guide. End-to-end PR review for a given PR number. | adharsh2208vthink |

---

## How to Update This File

When you open a PR with a new contribution, add a row to the relevant table above:

- **Name** — the `name` field from your frontmatter
- **File** — relative path from repo root (e.g., `skills/backend/my-skill.md`)
- **Description** — the `description` field from your frontmatter
- **Author** — your GitHub username

Reviewers will check that this file is updated as part of the PR review.
