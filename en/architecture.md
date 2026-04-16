# Vault for Founders: Architecture

> Design decisions and trade-offs behind the knowledge base structure.

---

## Design Principles

This architecture is built for founders. A founder's interaction with AI goes beyond chat or personal knowledge management — it involves company operations, product strategy, hiring, networking, and project management. The architecture needs to cover both "personal" and "company" dimensions.

Core trade-offs:

- **Less is more** — Folders and files are created only when needed, not pre-scaffolded as empty shells
- **Agent is the primary reader** — Structure, naming, and indexing prioritize LLM retrieval efficiency over human browsing habits
- **One file, one responsibility** — Persona settings, memory summaries, and company context are each independent, never mixed

---

## Folder Architecture and Rationale

### Root Directory (read on every startup)

| File | Responsibility |
|------|----------------|
| README.md | Vault index — the Agent uses this map to decide what to read |
| agent-persona.md | Agent's personality, collaboration style, communication norms |
| memory-summary.md | Distilled long-term memory: current focus, major decisions, lessons |

These three files are read on every Agent startup. Everything else is read as needed.

### Personal Dimension

| Folder | Purpose | When to create |
|--------|---------|----------------|
| identity/ | Founder's decision style, values, communication preferences | Day one |
| memory/ | Full record of each important decision | As major decisions happen |
| sop/ | Operating procedures (steps you forget when you haven't done them in a while) | When you ask about the same thing twice |

### Company Dimension

| Folder | Purpose | When to create |
|--------|---------|----------------|
| context/ | Company background, product strategy, competitive landscape, messaging | Day one |
| operations/ | Hard operational data (incorporation, banking, taxes) | When you have operations data |
| hr/ | Hiring and people, organized by cohort | When you start hiring |
| projects/ | Active projects (trips, events, market plans) | When you have multi-day projects |
| people/ | Key contacts — background and interaction notes | When your network gets complex |

---

## Agent Startup Sequence

Regardless of the tool (Cowork, OpenClaw, Claude Code), the Agent follows the same reading order on every startup:

1. **README.md** — Understand the Vault's structure and map
2. **agent-persona.md** — Understand its role and collaboration style
3. **memory-summary.md** — Quickly grasp recent priorities
4. Read additional folders as needed for the task at hand

This sequence is baked into the tool's custom instructions, so the Agent executes it automatically.

---

## How This Differs from Other Frameworks

Most AI knowledge base frameworks are designed for solo creators or freelancers, focused on personal life management and knowledge accumulation. Vault for Founders adds the company dimension that founders need: context, operations, hr, projects, people.

Another difference: the Agent isn't just a memory store — it's a cofounder. The persona design doesn't just define tone and style. It defines when the Agent should challenge the founder's thinking and when to defer. This upgrades the Agent from a tool to a thinking partner.

---

*Last updated: 2026/04/15*
