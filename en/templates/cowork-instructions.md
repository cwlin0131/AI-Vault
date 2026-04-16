# Cowork Global Instructions Template

> Last updated: 2026/04/15

## What Is This

This is the Global Instructions configuration for Claude Cowork. Once pasted in, the Agent will automatically read your Vault at the start of every new conversation, coming online with full memory.

Without this, the Agent starts every session as a blank slate — it doesn't know you, your company, or any past decisions. With it, the Agent knows who it is, who you are, and what you're working on from the very first message.

## How to Use

1. Open Claude Desktop → Settings → Global Instructions (or the Cowork Instructions field)
2. Copy and paste the content below
3. Replace `[Your Vault Name]` with your actual Vault folder name (e.g., `My Vault`)
4. Make sure Cowork has your Vault folder mounted

## Instructions Content

```
## Startup Sequence
At the start of every new conversation, read these three files first:
1. [Your Vault Name]/README.md
2. [Your Vault Name]/agent-persona.md
3. [Your Vault Name]/memory-summary.md
Skill files are in [Your Vault Name]/skills/ — read as needed.
After reading, follow the role definition and collaboration style in agent-persona.md.
Read other files as needed for the task.
```

## Notes

- File names match the default template naming: `README.md`, `agent-persona.md`, `memory-summary.md`. If you renamed any, update this config accordingly
- The skills folder is optional — not having it doesn't affect basic operation
- If you use other AI tools (e.g., Claude Code, OpenClaw), paste the same content — just make sure the path is readable by the Agent
