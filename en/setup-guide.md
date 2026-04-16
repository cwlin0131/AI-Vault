# Vault for Founders: Setup Guide

> A complete walkthrough for building an Obsidian + Git knowledge base from scratch. No technical background required.

---

## Prerequisites

You'll need:
- A computer (Windows or Mac)
- A GitHub account (free at https://github.com)

---

## Step 1: Install Git

Download and install from https://git-scm.com.

During installation, when you see "Adjusting your PATH environment," select **Git from the command line and also from 3rd-party software** (usually the default). Click Next for everything else.

After installation, **close all open terminal windows** and open a new one:
- **Windows**: Press `Win + R`, type `cmd`, press Enter
- **Mac**: Open Terminal from Applications → Utilities

Verify the installation:

```
git --version
```

If you see a version number, you're good.

### Configure Git Identity (one-time setup)

```
git config --global user.email "your-github-email@example.com"
git config --global user.name "your-github-username"
```

---

## Step 2: Install Obsidian

Download from https://obsidian.md and install. When you open it, select "Create new vault," give it a name, and choose a save location. Remember the Vault path — you'll need it later.

---

## Step 3: Create a Private Repo on GitHub

Go to https://github.com/new:

- Repository name: pick a name (e.g., `My-Vault`)
- Select **Private**
- Click Create

---

## Step 4: Connect Your Vault to GitHub

Open your terminal and run these commands (replace the path with your own):

```
cd "your-vault-path"
git init
git remote add origin https://github.com/your-username/your-repo-name.git
git branch -M main
```

---

## Step 5: Build the Folder Structure

Create the following folders in Obsidian (you can do this manually or ask your AI to help):

```
/
  README.md              ← Vault index, the first file your Agent reads
  agent-persona.md       ← Agent's role definition and collaboration style
  memory-summary.md      ← Long-term memory summary, read on every startup
  /identity              ← Who you are, values, decision style
  /context               ← Company background, product status, strategy
  /memory                ← Important decision records, meeting conclusions
  /sop                   ← Standard operating procedures
  /operations            ← Company operations data
  /projects              ← Project status tracking
  /people                ← Key contacts and backgrounds
```

Core files explained:

**README.md** is the Agent's navigation map. It lists the folder structure, reading order, and maintenance rules.

**agent-persona.md** is the Agent's soul. It defines its role, how it collaborates with you, communication style, and behavioral boundaries. This file determines whether the Agent is a "tool that follows instructions" or a "partner that can think with you."

**memory-summary.md** is the distilled version of long-term memory. After reading this on startup, the Agent can grasp your current focus, major decisions, and lessons learned in seconds.

Templates are available in the [templates/](templates/) folder.

---

## Step 6: First Push

```
git add .
git commit -m "init vault"
git push -u origin main
```

You may see a GitHub login prompt — just sign in. Once complete, check your GitHub repo page to confirm the files are uploaded.

---

## Step 7: Install Obsidian Git Plugin (Auto-Sync)

With this plugin, you don't need to run git commands manually. Obsidian will automatically back up to GitHub.

1. In Obsidian, click ⚙️ (bottom-left) → **Community plugins**
2. Turn off **Restricted mode**
3. Click "Browse" → search for **Obsidian Git**
4. Install [Vinzent03/obsidian-git](https://github.com/Vinzent03/obsidian-git) → Enable
5. In the plugin settings, set **Auto commit-and-sync interval** to `30` (auto-sync every 30 minutes)

Once configured, just write in Obsidian — it handles the rest.

---

## Daily Use

- Write notes and documents in Obsidian — everything syncs automatically
- To see change history, go to your GitHub repo and click "commits"
- When switching machines: install Git and Obsidian, run `git clone your-repo-url`, then open that folder in Obsidian

---

## Maintenance Principles

- One fact lives in one place only (Single Source of Truth)
- Search before creating a new file
- Mark the last-updated date at the top of every document
- Never put sensitive information (API keys, passwords, etc.) in the repo

---

*Last updated: 2026/04/15*
