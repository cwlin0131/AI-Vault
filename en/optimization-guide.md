# Vault Optimization Guide — Help Your Agent Find the Right Files Faster

> After building your Vault, retrieval efficiency degrades as files accumulate. This guide covers practical optimization techniques based on real experience.

---

## Core Concept

The primary reader of your Vault is an AI Agent, not a human. Every optimization here serves one goal: **reduce the cost for the Agent to find the right file.**

The Agent's behavior on every startup: read README → decide which files are needed → open and read them. If you can make the first step precise, it won't waste time opening the wrong files.

---

## 1. README Is the Agent's Map

README is the first file the Agent reads on every startup. It uses this index to decide whether to open each file.

**How to do it:**
- Don't just describe folders — go to the granularity of every single file, with a one-line summary each
- The summary describes the file's content, not a repetition of the filename
- When you add, delete, or move files, update the README in sync

**Bad example:**
```
├── /operations
│   └── entity.md          ← Company data
```
The Agent sees "company data" but doesn't know if it's incorporation docs, bank accounts, or tax filings.

**Good example:**
```
├── /operations
│   └── corp-setup.md      ← Delaware C Corp incorporation data, EIN status, bank account setup
```
The Agent immediately knows this is about incorporation — no need to open the file to check.

---

## 2. Filenames Are the Index

Good filenames let the Agent decide whether to read a file just by looking at the file list, without relying on README or opening the file.

**Naming rules:**
- Avoid generic names — use descriptive filenames (`corp-setup.md` instead of `entity.md`)
- For files in the same category, use `topic-subtopic` format with the topic first (`product-roadmap.md`, `product-pricing.md`)
- Memory files: use `YYYY-MM-DD_topic-summary.md` (dates for easy sorting)
- Project folders: use `YYYY-MM-topic/`

**Write your naming rules into the README** so both your future self and the Agent follow the same standard.

---

## 3. YAML Frontmatter Tagging

Add YAML frontmatter at the top of every `.md` file so the Agent can assess a file's nature and freshness without reading the entire thing.

**You only need three fields:**

```yaml
---
updated: 2026-04-15
tags: [context, product, strategy]
summary: 90-day expansion strategy — positioning, channels, pricing, milestones
---
```

- `updated` — Last modified date, so the Agent can judge information freshness
- `tags` — Category labels for search and cross-referencing
- `summary` — One-line summary, kept consistent with the README index description

**Don't add too many metadata fields.** The more fields you have, the higher the maintenance cost. You'll start skipping updates, and eventually the metadata becomes less accurate than the content itself. Three fields is enough.

---

## 4. Memory Summary Periodic Cleanup

`memory-summary.md` is read by the Agent on every startup. If you don't clean it periodically, stale information will mislead the Agent's judgment.

**Cleanup rules:**
- After completing a task, go back and update the result column or remove items that are no longer relevant
- Periodically check for duplicates, outdated entries, or items whose status has changed
- Review before deleting — confirm with yourself to avoid removing items that are still important but look old

**Suggested frequency:** Once a week, or after every major decision. Doesn't need to be too frequent, but can't be never.

---

## Execution Order Matters

If you're doing multiple optimizations at once, follow this order:

1. **Rename files first** — Change vague names to descriptive ones
2. **Then write the README index and frontmatter** — Based on final filenames, so you don't have to do it twice
3. **Run a verification pass last** — Confirm all internal links and references point to the new filenames

Rename first, then index — avoid double work.

---

## When to Do This

- **Right after building your Vault** — No rush. Accumulate some files first
- **When you pass 10 files** — Worth investing in README index enhancement and frontmatter
- **When you notice the Agent opening wrong files** — The index isn't clear enough, time to optimize
- **Every time you add a new file** — Update the README and add frontmatter as you go. Building the habit is more effective than one big cleanup session
