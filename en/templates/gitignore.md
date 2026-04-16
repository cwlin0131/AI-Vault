# .gitignore Template (Obsidian Vault)

> Last updated: 2026/04/17

## What This Is

`.gitignore` is a standard Git config file placed in your Vault root. It tells Git which files to skip, so local-only settings, caches, and junk files don't end up in your repo.

## Why You Need It

Obsidian creates a `.obsidian/` folder inside your Vault, containing **machine-local preferences** (graph view, hotkeys, installed plugins, workspace tabs, etc.). These:

- **Should not be shared across machines** — each machine has its own preferences
- **Are modified by plugins automatically** — a major source of constant cross-machine conflicts
- **Include plugin code itself** (e.g., `obsidian-git/main.js`) — plugin upgrades create massive diffs

Operating systems also produce junk files (`.DS_Store`, `Thumbs.db`) that don't belong in your repo.

**No `.gitignore` = `.obsidian/` tracked = never-ending conflicts.**

## How to Use

1. Create a file named `.gitignore` (note the leading dot) in your Vault root
2. Copy the "Config Content" below into it and save
3. If `.obsidian/` was already tracked by Git, run:
   ```bash
   git rm -r --cached .obsidian/
   git commit -m "chore: stop tracking .obsidian/ (local settings)"
   ```
4. This doesn't delete `.obsidian/` from your disk — it just tells Git to ignore it going forward

## Config Content

```
# Obsidian local settings (app preferences, plugins, hotkeys, graph, workspace, etc.)
# Not shared across machines; each machine manages its own.
.obsidian/

# macOS
.DS_Store

# Windows
Thumbs.db
desktop.ini

# Editor scratch files
*.swp
*.swo
*~
.vscode/
.idea/
```

## If You Want to Sync Some Obsidian Settings Across Machines

Common cases: you want to sync hotkeys or the installed plugin list. Two options:

**Option A: Don't ignore at all (not recommended)**
Delete the `.obsidian/` line from `.gitignore`. The cost is frequent conflicts. Not worth it.

**Option B: Selective ignore (advanced)**
Ignore only workspace state and plugin binaries, keep the config files:
```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/*/main.js
.obsidian/plugins/*/styles.css
.obsidian/cache
```
This keeps `hotkeys.json`, `community-plugins.json`, and similar config synced.

**For most people, just ignore all of `.obsidian/`.** Resetting hotkeys once takes 30 seconds and you get stability in return.

## Notes

- After committing, **every collaborating machine must pull once** for the new rules to take effect.
- Pair this with `.gitattributes` (see sibling template) for the complete cross-machine sync fix.
