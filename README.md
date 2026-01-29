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
git clone <REPO_URL> /tmp/cursor-config
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