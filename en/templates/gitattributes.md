# .gitattributes Template

> Last updated: 2026/04/17

## What This Is

`.gitattributes` is a standard Git config file placed in your Vault root. It tells Git how to handle each file, particularly **line ending rules**.

## Why You Need It

When you start syncing the same Vault across multiple machines and multiple tools (Obsidian Git, GitHub Desktop, Claude Code, Cursor), different tools handle line endings differently:

- Mac / Linux default to **LF** (`\n`)
- Windows defaults to **CRLF** (`\r\n`)

They look identical to humans but are different bytes to Git. If one tool flips the format, other machines pulling the repo see a fake diff claiming every line changed, triggering merge conflicts.

**No `.gitattributes` = sync conflicts will eventually happen.**

## How to Use

1. Create a file named `.gitattributes` (note the leading dot) in your Vault root
2. Copy the "Config Content" below into it and save
3. First time adding:
   ```bash
   git add .gitattributes
   git commit -m "chore: add .gitattributes (enforce LF line endings)"
   ```
4. Optional: if the repo already contains files saved as CRLF, run `git add --renormalize .` once to convert everything to LF

## Config Content

```
# Enforce LF line endings for all text files to avoid cross-machine / cross-tool conflicts.
# After enabling, run once: git add --renormalize .

* text=auto eol=lf

# Explicitly mark as text (LF)
*.md       text eol=lf
*.txt      text eol=lf
*.json     text eol=lf
*.js       text eol=lf
*.ts       text eol=lf
*.py       text eol=lf
*.yml      text eol=lf
*.yaml     text eol=lf
*.xml      text eol=lf
*.html     text eol=lf
*.css      text eol=lf
*.sh       text eol=lf
.gitignore text eol=lf
.gitattributes text eol=lf

# Binary files, no line-ending conversion
*.png      binary
*.jpg      binary
*.jpeg     binary
*.gif      binary
*.ico      binary
*.svg      binary
*.pdf      binary
*.docx     binary
*.pptx     binary
*.xlsx     binary
*.zip      binary
*.gz       binary
*.woff     binary
*.woff2    binary
*.ttf      binary
*.otf      binary
*.mp3      binary
*.mp4      binary
*.mov      binary
```

## Notes

- This config targets **Markdown knowledge bases**. If your Vault contains special file types, extend as needed.
- After committing, **every collaborating machine must pull once** for the new rules to take effect.
- Older files may appear as a one-time large diff. That's the normalization pass, not actual content change.
