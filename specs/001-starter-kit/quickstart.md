# Quickstart: Starter Repo Kit

**Branch**: `001-starter-kit` | **Date**: 2026-03-16

## Prerequisites

- macOS or Windows computer
- Claude account with a paid plan ($20/month Claude Pro is the cheapest option; Max, Team, and Enterprise also work)
- GitHub account (free)
- Internet connection

## Field Guide (read first)

Before starting setup, open `field-guide.html` from the repo: go to https://raw.githubusercontent.com/zleavitt-401/starter-repo/main/field-guide.html and save it locally (or use the live Pages link once available — see "Field Guide" below). It's a plain-English glossary of terms used throughout this guide (repo, clone, fork, terminal, etc.) for readers with no coding background.

## Setup (for the recipient)

1. Create a Claude account at claude.ai and subscribe to a paid plan; also create a free GitHub account at github.com/join if you don't have one
2. Install the Claude app from claude.com/download, then sign in (Windows: Git for Windows is required for local sessions — the app prompts if it's missing). The app has three tabs — Chat (conversation, with Artifacts for anything substantial Claude produces), Cowork (semi-autonomous file production), and Code (Claude Code, used for all of the below)
3. Fork the repo on GitHub (github.com/zleavitt-401/starter-repo → **Fork**), then clone your fork:
   ```
   git clone https://github.com/<your-github-username>/starter-repo ~/.claude
   ```
4. In the Claude app, click the **Code** tab, choose **Local**, and select the `~/.claude` folder
5. Pick a model and leave the permission mode on **Manual**
6. In the Code tab's chat, type `/starter`, follow the prompts

VS Code remains available as an optional add-on (see the README's "Optional: Set up VS Code too" section) but isn't required for any of the above.

## Verification

After `/starter` completes, verify:
- Type `/` in Claude Code → all commands visible
- Skills are loaded (Claude can reference them in any project)
- `gh auth status` shows logged in
- `vercel whoami` shows logged in

## Updating

```
cd ~/.claude && git pull
```

## Adding personal skills

Create a new folder in `~/.claude/skills/` with a `SKILL.md` file.
It will be ignored by git and survive `git pull`.

## Using skills in claude.ai chat

Skills in `~/.claude/skills/` only run automatically in Claude Code — they don't carry over to claude.ai chat automatically. To use one in chat: enable "code execution and file creation" in claude.ai Settings → Capabilities, then Settings → Capabilities → Skills → + → Create skill → Upload a skill, and upload a zip of the skill folder. Private per account; one-time per skill. Skills that hand off to Claude Code slash commands (e.g. `implementation-prompt-generator` → `/speckit.specify`) only complete that hand-off inside Claude Code.

## Field Guide

Visit: https://\<your-github-username>.github.io/starter-repo (after enabling GitHub Pages on your fork)
