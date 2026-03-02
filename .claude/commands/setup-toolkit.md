---
name: setup-toolkit
description: >
  Analyze the current project and recommend which toolkit items (skills, agents,
  commands, hooks, MCP configs, settings template) are relevant. Then install
  the approved ones into the project's .claude/ directory. Invoke with /setup-toolkit.
version: 0.1.0-draft
author: adharsh2208vthink
category: utility
tags: [setup, import, install, onboarding]
---

# Toolkit Setup Wizard

Analyzes the current project and installs only the toolkit items that are relevant to it.

## Prerequisites

This command assumes the `vthink-claudecode-toolkit` repo is cloned somewhere on the machine.
Ask the user for the path if not obvious:
> "Where is the vthink-claudecode-toolkit cloned? (e.g., ~/git/vthink-claudecode-toolkit)"

Store the path as `$TOOLKIT_PATH` for use throughout.

---

## Step 1: Scan the Project

Gather signals about the project's tech stack and workflow by reading:

| File | What it tells us |
|------|-----------------|
| `package.json` | Node/JS project, framework (React, Express, Next.js), test runner (jest, vitest) |
| `pom.xml` | Java/Maven project, Spring Boot |
| `requirements.txt` / `pyproject.toml` | Python project, frameworks (Django, Flask, FastAPI) |
| `build.gradle` | Java/Gradle project |
| `.github/workflows/` | CI/CD setup, whether PRs go through GitHub Actions |
| `CLAUDE.md` | Existing Claude Code setup, any already-installed tools |
| `.claude/settings.json` | Already configured permissions and hooks |
| `.claude/skills/`, `.claude/agents/`, `.claude/commands/` | Already installed toolkit items |

Also check the project's git remote to determine if it's a GitHub repo (relevant for `qa-guide`, `conventions-check` PR mode).

---

## Step 2: Evaluate Each Toolkit Item

For each item in the catalog below, determine **Recommended / Optional / Not relevant** based on the project signals:

### Skills

| Skill | Recommend if... |
|-------|----------------|
| `anonymize-prompt` | Always — useful for any project |
| `bdd-gherkin` | Project has a QA process, `.feature` files exist, or team does acceptance testing |
| `commit-push` | Project uses git (always) |
| `conventions-check` | Project has a linter config (`.eslintrc`, `checkstyle.xml`, etc.) or `CLAUDE.md` conventions |
| `give-me-a-commit-message` | Project uses git (always) |
| `qa-guide` | Project has a GitHub remote and does PRs |
| `ship` | Project uses git and GitHub (always) |
| `generate-endpoint` | Project has a backend with routes (`app.js`, `routes/`, `controllers/`, Flask/Django views) |

### Agents

| Agent | Recommend if... |
|-------|----------------|
| `test-runner` | `package.json` has a `test` script, or `pytest`/`mvn test` is detectable |

### Commands

| Command | Recommend if... |
|---------|----------------|
| `dev-server` | `package.json` has a `start` or `dev` script, or a known dev server pattern exists |

### Hooks

| Hook | Recommend if... |
|------|----------------|
| `check-naming-conventions.sh` | Project has source files and would benefit from naming guard rails |

### MCP Configs

| Config | Recommend if... |
|--------|----------------|
| `github` | Project has a GitHub remote |
| `postgres` | `package.json` deps or requirements include a Postgres driver (`pg`, `psycopg2`, `postgresql`) |
| `sqlite` | Project has a `.db` file or deps include `sqlite3`, `better-sqlite3` |
| `puppeteer` | Project has E2E tests (Playwright/Puppeteer deps) or is a web scraping project |
| `filesystem` | Project is part of a monorepo or needs access to sibling directories |

### Settings Templates

| Template | Recommend if... |
|----------|----------------|
| `nodejs` | `package.json` exists, no frontend framework detected |
| `react` | `package.json` includes `react`, `next`, `vite`, or `react-scripts` |
| `python` | `requirements.txt` or `pyproject.toml` exists |
| `java-spring` | `pom.xml` exists with Spring dependencies |

---

## Step 3: Present Recommendations

Show a clear summary grouped by category:

```
## Toolkit Recommendations for <project-name>

Detected: Node.js / Express backend, GitHub remote, Jest test suite

### Recommended (high relevance)
- [x] skill: ship
- [x] skill: commit-push
- [x] skill: give-me-a-commit-message
- [x] skill: conventions-check
- [x] skill: qa-guide
- [x] agent: test-runner
- [x] command: dev-server
- [x] hook: check-naming-conventions.sh
- [x] mcp: github
- [x] settings-template: nodejs

### Optional (may be useful)
- [ ] skill: anonymize-prompt
- [ ] skill: bdd-gherkin
- [ ] skill: generate-endpoint

### Not relevant (skipping)
- mcp: postgres (no Postgres dependency detected)
- mcp: sqlite (no SQLite dependency detected)
- settings-template: react (not a React project)
- settings-template: python (not a Python project)
- settings-template: java-spring (not a Java project)

Which items would you like to install? You can adjust the checkboxes above.
```

Use `AskUserQuestion` to let the user confirm or adjust the selection.

---

## Step 4: Install Approved Items

For each approved item, copy it to the correct location in the current project:

```bash
# Skills
mkdir -p .claude/skills
cp $TOOLKIT_PATH/skills/<category>/<skill>.md .claude/skills/

# Agents
mkdir -p .claude/agents
cp $TOOLKIT_PATH/agents/<category>/<agent>.md .claude/agents/

# Commands
mkdir -p .claude/commands
cp $TOOLKIT_PATH/.claude/commands/<command>.md .claude/commands/

# Hooks
mkdir -p .claude/hooks/pre-tool
cp $TOOLKIT_PATH/hooks/pre-tool/<hook>.sh .claude/hooks/pre-tool/
chmod +x .claude/hooks/pre-tool/<hook>.sh

# MCP config — extract the mcpServers block and merge into .claude/settings.json
# (see Step 4a below)

# Settings template — copy as .claude/settings.json if none exists
# (see Step 4b below)
```

### Step 4a: MCP Config Merge

If `settings.json` already exists, **merge** the new `mcpServers` entry into it — do not overwrite the whole file. Read the existing file, add the new server block under `mcpServers`, and write it back.

If `settings.json` does not exist, create it with just the `mcpServers` block.

### Step 4b: Settings Template

If a settings template was selected:
- If `.claude/settings.json` **does not exist**: copy the template as the new settings file (strip the `_readme`, `_usage`, `_hook_note` keys first)
- If `.claude/settings.json` **already exists**: show a diff of what would change and ask the user if they want to merge the `permissions` block

---

## Step 5: Summary

After installation, print a final summary:

```
## Setup Complete

Installed into .claude/:
  skills/  → ship.md, commit-push.md, give-me-a-commit-message.md, conventions-check.md, qa-guide.md
  agents/  → test-runner.md
  commands/ → dev-server.md
  hooks/pre-tool/ → check-naming-conventions.sh
  settings.json → nodejs template applied, github MCP added

Next steps:
  1. Set GITHUB_TOKEN env var for the GitHub MCP server
  2. Restart Claude Code to activate the new tools
  3. Try /dev-server start to test the server command
```
