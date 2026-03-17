---
description: First-time environment setup — installs Vercel CLI, GitHub CLI, connects GitHub and Vercel, and verifies everything is ready
---

# /starter — New Developer Environment Setup

You are helping a brand new developer finish setting up their environment. This repo has already been cloned to ~/.claude, so commands and skills are already in place. Node.js and Claude Code are already installed. Do everything else for them.

Work through each step in order. Run the command, check the result, fix any errors before moving on. Be encouraging and explain what each step is doing in plain language — this person is new to coding.

---

## Step 1: Pull latest files

Make sure the local copy of starter-repo is up to date before doing anything else.

```bash
cd ~/.claude && git pull
```

- Pulls cleanly → ✅ continue
- "not a git repository" → something went wrong during cloning. Tell the user: "It looks like ~/.claude wasn't set up as a git repo. Please re-run the clone step from the README and try /starter again."
- Merge conflict → tell the user: "There's a conflict with a file you've changed locally. Let's fix that first." Help them resolve it.

---

## Step 2: Verify Node.js is working

```bash
node --version && npm --version
```

- Both print version numbers → ✅ continue
- "command not found" → stop and tell the user: "Node.js doesn't seem to be installed yet. Please go to https://nodejs.org, download the LTS version, install it, then restart VS Code and try /starter again."

---

## Step 3: Install GitHub CLI

```bash
gh --version
```

- Already installed → ✅ skip to Step 4
- Not found → install it:

**Mac:**
```bash
brew install gh
```

If brew is not installed, install it first:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Then retry `brew install gh`.

**Windows** (if winget is available):
```bash
winget install GitHub.cli
```

If neither works, tell the user: "Please install GitHub CLI manually from https://cli.github.com, then restart VS Code and continue."

---

## Step 4: Log into GitHub

```bash
gh auth status
```

- Already logged in → ✅ skip to Step 5
- Not logged in → run:
```bash
gh auth login
```
Choose: GitHub.com → HTTPS → Login with a web browser. A browser window will open — complete the login there, then return here.

---

## Step 5: Set Git identity (if not already set)

```bash
git config --global user.name && git config --global user.email
```

- Both return values → ✅ skip to Step 6
- Either is blank → ask the user for their name and email, then run:
```bash
git config --global user.name "Their Name"
git config --global user.email "their@email.com"
```

---

## Step 6: Install Vercel CLI

```bash
vercel --version
```

- Already installed → ✅ skip to Step 7
- Not found → install:
```bash
npm install -g vercel
```

---

## Step 7: Log into Vercel

```bash
vercel whoami
```

- Already logged in → ✅ skip to Step 8
- Not logged in → run:
```bash
vercel login
```
A browser window will open. Log in with the same account used on vercel.com, then return here.

---

## Step 8: Final check

```bash
echo "✅ Node: $(node --version)"
echo "✅ Git user: $(git config --global user.name)"
echo "✅ GitHub: $(gh auth status 2>&1 | grep 'Logged in' || echo 'check needed')"
echo "✅ Vercel: $(vercel whoami 2>/dev/null || echo 'check needed')"
echo "✅ Commands: $(ls ~/.claude/commands/ 2>/dev/null | wc -l | tr -d ' ') installed"
echo "✅ Skills: $(ls ~/.claude/skills/ 2>/dev/null | wc -l | tr -d ' ') installed"
```

All lines show values → 🎉 tell the user:

> "You're all set! Here's how to start your first project: type **/new-project** right here in Claude Code. That command will walk you through creating your first app and connecting it to GitHub and Vercel."

---

## If anything goes wrong

- `permission denied` on npm install → try the command again with `sudo` at the front (Mac only)
- Browser login window doesn't open → try running the login command again
- `git pull` fails with "divergent branches" → run `git pull --rebase` instead
