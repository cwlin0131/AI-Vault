# Memory Scaling Guide — When Your Memory Outgrows a Single File

> Your Vault has been running for three months. `memory-summary.md` grew from 30 lines to 200. The Agent takes longer to start, and keeps acting on outdated information. This guide covers what to do at this stage.

---

## The Problem: One File Can't Hold It All

`memory-summary.md` is designed as a "startup essentials" file the Agent reads every session. But as decisions accumulate:

- **Too long** — The Agent burns through tokens just reading memory, slowing down responses
- **Too noisy** — Three-month-old decisions sit next to today's priorities, confusing the Agent
- **Too stale** — Completed projects still listed, misleading the Agent's judgment
- **Too risky to edit** — Every cleanup risks deleting something still important

This isn't a discipline problem — it's an architecture problem. One file acting as both index and content will always hit a wall.

---

## The Fix: Two-Layer Memory

Split `memory-summary.md` into two layers:

```
memory-summary.md        ← Index layer (≤50 lines): pointers only, no content
memory/
├── active-focus.md      ← Current focus (1-3 things)
├── decisions/
│   ├── 2026-01_product-pivot.md
│   └── 2026-03_pricing-change.md
├── lessons.md           ← Accumulated lessons
├── patterns.md          ← Patterns the Agent has observed
└── archive/             ← Completed or expired decisions
```

### Index Layer: memory-summary.md

Becomes a pure routing table — one pointer per line, under 50 lines:

```markdown
# Memory Summary

> Last updated: 2026/04/15
> This is an index, not content. Agent reads this to decide which memory/ files to open.

## Current Focus
→ [memory/active-focus.md](memory/active-focus.md)

## Key Decisions (newest first)
- [2026-03 Pricing Change](memory/decisions/2026-03_pricing-change.md) — B2B to PLG, $29/mo → $9/mo
- [2026-01 Product Pivot](memory/decisions/2026-01_product-pivot.md) — Dashboard → API-first

## Lessons
→ [memory/lessons.md](memory/lessons.md)

## My Patterns
→ [memory/patterns.md](memory/patterns.md)

## Archive (completed / expired)
→ [memory/archive/](memory/archive/)
```

### Content Layer: memory/*.md

Each file owns one topic. Use frontmatter to mark freshness:

```markdown
---
updated: 2026-03-20
status: active        # active / archived
tags: [pricing, strategy]
summary: B2B to PLG pricing shift, $29→$9/mo
---

# 2026-03 Pricing Change

## Background
(...)

## Decision
(...)

## Outcome
(...)
```

---

## When to Switch to Two Layers

You don't need two layers from day one. Here's when to switch:

| State | Action |
|-------|--------|
| memory-summary.md < 50 lines | Stay as-is |
| memory-summary.md 50-100 lines | Consider splitting, not urgent |
| memory-summary.md > 100 lines | Time to split — Agent efficiency is dropping |
| Agent starts acting on stale info | Split now, don't wait |

---

## Memory Decay: What Stays, What Gets Archived

Not all memories stay important forever. Periodically ask yourself:

**Keep active:**
- Decisions related to ongoing projects
- Lessons that have been validated repeatedly
- Preferences the Agent needs to know every session

**Move to archive:**
- Decisions from completed projects (outcome known, no impact on current work)
- Old decisions superseded by newer ones
- Items untouched for 6+ months

**Archiving is not deleting.** Files stay in `memory/archive/` — the Agent can reference them when needed. They just won't be read at startup.

---

## Agent-Assisted Cleanup

Add this to `agent-persona.md` so the Agent helps maintain memory:

```markdown
## Memory Maintenance
- After reading memory-summary.md, if it exceeds 50 lines, remind me to do a cleanup
- If you find completed items still in the active section, suggest archiving them
- After recording a new decision, update memory-summary.md index
- When archiving, tell me what you archived so I can confirm
```

---

## Integration with After-Action Reviews

Memory records produced by the after-action flow go directly into `memory/decisions/`. Then add one index line to `memory-summary.md`.

This way the after-action process doesn't bloat the summary — the `memory/` folder grows (which is fine), while the summary only adds one line.

---

## Where This Pattern Comes From

This two-layer memory architecture comes from running a multi-agent AI system (19 agents, 50+ memory files) for over 6 months. When the memory index file grew to 200 lines, we found:

1. The Agent spent too much of its context window just reading the index
2. Stale info mixed with current priorities caused the Agent to misjudge relevance
3. Manual cleanup took 30+ minutes each time, so it happened less and less

After splitting into index layer + content layer, the index stayed under 50 lines, Agent startup became faster, and maintenance effort dropped significantly.

---

*Last updated: 2026/04/16*
