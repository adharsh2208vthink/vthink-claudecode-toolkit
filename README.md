# vthink-claudecode-toolkit

> A shared toolkit of Claude Code skills, agents, slash commands, and hooks for the vthink engineering team.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Claude Code](https://img.shields.io/badge/Claude_Code-compatible-blue)](https://github.com/anthropics/claude-code)

---

## What's in the Toolkit

Browse the full catalog: **[CATALOG.md](CATALOG.md)**

| Category | Count | Location |
|----------|-------|----------|
| Agents | — | [`agents/`](agents/) |
| Skills | — | [`skills/`](skills/) |
| Slash Commands | — | [`commands/`](commands/) |
| Hooks | — | [`hooks/`](hooks/) |
| Rules | — | [`rules/`](rules/) |
| MCP Configs | — | [`mcp/`](mcp/) |
| Settings Templates | — | [`settings-templates/`](settings-templates/) |
| Workflows | — | [`workflows/`](workflows/) |

---

## Quick Install

### The fast way — let the setup wizard do it

Install the setup wizard once, globally. It becomes available in every project on your machine:

```bash
mkdir -p ~/.claude/agents
cp path/to/vthink-claudecode-toolkit/agents/utility/setup-wizard.md ~/.claude/agents/
```

Then open any project in Claude Code and say:

> *"Set up the vthink toolkit for this project"*

The wizard will ask you a few questions, scan your project, and install only what's relevant to *you*.

### Manual install

If you prefer to pick and install items yourself:

```bash
# Copy a single skill
cp path/to/vthink-claudecode-toolkit/skills/backend/my-skill.md \
   your-project/.claude/skills/

# Copy all slash commands
cp vthink-claudecode-toolkit/commands/*.md \
   your-project/.claude/commands/

# Copy and enable a hook
cp vthink-claudecode-toolkit/hooks/pre-tool/my-hook.sh \
   your-project/.claude/hooks/pre-tool/
chmod +x your-project/.claude/hooks/pre-tool/my-hook.sh
```

> See [`docs/getting-started.md`](docs/getting-started.md) for a full walkthrough.

---

## Directory Guide

```
vthink-claudecode-toolkit/
├── commands/               # Slash commands — copy to your-project/.claude/commands/
├── agents/                 # Sub-agent definitions, organized by category
│   ├── core-development/
│   ├── code-review/
│   ├── testing/
│   ├── devops/
│   └── utility/            # Toolkit-level agents (e.g., setup-wizard)
├── skills/                 # Skill files — domain/workflow knowledge for Claude
│   ├── frontend/
│   ├── backend/
│   └── data/
├── hooks/                  # Shell scripts triggered by Claude Code events
│   ├── pre-tool/           # Run before a tool executes
│   └── post-tool/          # Run after a tool executes
├── rules/                  # CLAUDE.md snippets — always-follow instructions
├── mcp/                    # MCP server config snippets (copy into settings.json)
├── settings-templates/     # Pre-built .claude/settings.json by project type
├── workflows/              # Multi-agent orchestration patterns
├── templates/              # Starter templates for new contributions
├── examples/               # Real-world usage examples
└── docs/                   # Documentation
```

---

## Featured Contributions

_Add standout skills, agents, or commands here as the toolkit grows._

---

## How to Contribute

We welcome contributions from any vthink engineer! See [CONTRIBUTING.md](CONTRIBUTING.md) for:

- Standards for file naming and frontmatter
- Which folder your contribution belongs in
- How to use the starter templates
- The PR review process

---

## License

[MIT](LICENSE)
