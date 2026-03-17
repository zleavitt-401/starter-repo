# Quickstart: Starter Repo Kit

**Branch**: `001-starter-kit` | **Date**: 2026-03-16

## Prerequisites

- macOS computer
- Claude Pro account ($20/month at claude.ai)
- Internet connection

## Setup (for the recipient)

1. Install VS Code from code.visualstudio.com
2. Install Node.js LTS from nodejs.org
3. Clone the repo:
   ```
   git clone https://github.com/zleavitt-401/starter-repo ~/.claude
   ```
4. Open VS Code
5. Install Claude Code extension (by Anthropic) from Extensions sidebar
6. Enable Bypass Permissions in VS Code Settings
7. Install recommended extensions: GitLens, Prettier, Live Server, Error Lens
8. Open Claude Code panel, type `/starter`, follow the prompts

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
