# Cowork Global Instructions Template

> Last updated: 2026/04/17 (v3: added Forced Rules section)

## What Is This

This is the Global Instructions configuration for Claude Cowork / OpenClaw. Once pasted in, the Agent will automatically read your Vault at the start of every new conversation, coming online with full memory.

Without this, the Agent starts every session as a blank slate. It doesn't know you, your company, or any past decisions. With it, the Agent knows who it is, who you are, and what you're working on from the very first message.

## How to Use

1. Open Claude Cowork (or OpenClaw) → Settings → Global Instructions
2. Copy and paste the content below
3. Replace `[Your Vault Name]` with your actual Vault folder name (e.g., `My Vault`)
4. Make sure Cowork has your Vault folder mounted
5. **Every machine needs its own setup** (global instructions don't sync across machines)

## Instructions Content

```
## Startup Sequence
At the start of every new conversation, read these three files first:
1. [Your Vault Name]/README.md
2. [Your Vault Name]/agent-persona.md
3. [Your Vault Name]/memory-summary.md

Skill files are in [Your Vault Name]/skills/ — read as needed.
After reading, follow the role definition and collaboration style in agent-persona.md.

## Forced Rules (not suggestions; required for task completion)
1. Vault Index Sync: after adding, deleting, or moving files or folders inside the Vault, update the root README.md (file tree + last-updated date) in the same response.
2. Writing Rules for Public Content: before drafting any public-facing writing (LinkedIn, README, press, pitch, landing copy, etc.), read [Your Vault Name]/templates/voice-and-tone.md (if present) and follow its rules.

After significant tasks, remind the user to run the after-action routine.
Read other files as needed for the task.
```

## Why Have a "Forced Rules" Section

Relying on the AI to just "remember" these rules over time is unreliable. In practice:

- Creating a new file and forgetting to update the README → index drifts → Agent starts missing files
- Drafting public writing without checking voice rules → output doesn't sound like the founder
- Finishing a task without capturing the decision → important context is lost

Putting these as **Forced Rules at the Global Instructions level** (not buried in some SOP file) is currently the most reliable approach, because global instructions are **read at the start of every new conversation** — the highest-priority context.

## Layered Defense (Advanced)

If you want a more complete "nothing falls through the cracks" architecture, stack these layers:

1. **First layer (active trigger)**: Global Instructions Forced Rules ← this file
2. **Second layer (safety net)**: After-action SOP (`after-action.md` template) checks again at task close
3. **Third layer (periodic health check)**: A custom vault-audit SOP that periodically scans the README index for drift (not included in this template set, build your own when needed)
4. **Background discipline**: Forced Rules section in the Vault README

All four layers stacked minimize the miss rate. **You don't need all of them day one.** Set up the Global Instructions layer first. If you find rules still slip through, add the next layer.

## Notes

- File names match the default template naming: `README.md`, `agent-persona.md`, `memory-summary.md`. If you renamed any, update this config accordingly.
- The skills folder is optional. Not having it doesn't affect basic operation.
- If you use other AI tools (e.g., Claude Code), paste the same content. Just confirm the path is readable by the Agent.
- When rules evolve, **remember to update the Global Instructions on every machine**. That's the easiest thing to forget.
