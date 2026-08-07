# Quickstart: Starter Repo Kit

**Branch**: `001-starter-kit` | **Date**: 2026-03-16

## Prerequisites

- macOS or Windows computer
- Claude account with a paid plan ($20/month Claude Pro is the cheapest option; Max, Team, and Enterprise also work)
- Internet connection

## Setup (for the recipient)

1. Create a Claude account at claude.ai and subscribe to a paid plan
2. Install the Claude app from claude.com/download, then sign in (Windows: Git for Windows is required for local sessions — the app prompts if it's missing)
3. Clone the repo:
   ```
   git clone https://github.com/zleavitt-401/starter-repo ~/.claude
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

## Field Guide

Visit: https://zleavitt-401.github.io/starter-repo
