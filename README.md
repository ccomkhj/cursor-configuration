# .cursor (Personal Cursor Config)

Personal Cursor configuration + helper scripts used across projects.

This repo is designed to be **portable** (easy to set up on a new machine) and **safe** (no credentials or noisy artifacts tracked).

---

## Contents

Typical structure:

- `skills/` 
- `commands/` 
- `.gitignore` — **critical**: prevents secret leakage + unnecessary tracking
- `README.md`

---

## Setup (safe / additive clone)

⚠️ Do **not** clone directly into `~/.cursor` (Git clone is not additive and may overwrite local state).

Instead:

```bash
git clone https://github.com/ccomkhj/cursor-configuration /tmp/cursor-config
mkdir -p ~/.cursor
rsync -av --ignore-existing /tmp/cursor-config/ ~/.cursor/
````

Preview before applying (recommended):

```bash
rsync -av --dry-run /tmp/cursor-config/ ~/.cursor/
```

If you intentionally want to overwrite tracked config files:

```bash
rsync -av /tmp/cursor-config/ ~/.cursor/
```

---

## Security / `.gitignore` policy

This directory can easily contain sensitive or machine-specific files (API keys, tokens, `.env`, logs, caches).
To prevent credential leakage and reduce noise:

* keep `.gitignore` strict
* never commit secrets
* treat unknown files as unsafe by default

**Never commit:**

* `.env`, `.env.*`
* API keys / tokens
* private keys (`*.pem`, `*.key`, etc.)
* logs, reports, caches, outputs

---

### New to the setup? Read below.

- Rules provide system-level instructions to Agent. They bundle prompts, scripts, and more together, making it easy to manage and share workflows across your team.
- Custom commands allow you to create reusable workflows that can be triggered with a simple / prefix in the chat input box.
- Agent Skills is an open standard for extending AI agents with specialized capabilities. Skills package domain-specific knowledge and workflows that agents can use to perform specific tasks.
    - [openskills](https://github.com/numman-ali/openskills)
- Subagents are specialized AI assistants that Cursor's agent can delegate tasks to. Each subagent operates in its own context window, handles specific types of work, and returns its result to the parent agent. Use subagents to break down complex tasks, do work in parallel, and preserve context in the main conversation.
- Semantic search finds code by understanding its meaning, not just matching text. Ask natural language questions like "where is authentication handled?" and get relevant results across your entire codebase.
- Model Context Protocol (MCP) enables Cursor to connect to external tools and data sources.
    - [fastmcp](https://github.com/jlowin/fastmcp)