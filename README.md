# Starter Repo

Everything you need to start building with Claude — commands, skills, and a field guide — in one place.

This repo is designed to be cloned once to a special folder on your computer. After that, Claude — in the Claude app's **Code** tab — will have access to all the tools and shortcuts included here. No coding experience required.

New to coding entirely? Read "Before you start: open the field guide" below before anything else — it's a plain-English glossary for every unfamiliar term you're about to run into.

---

## What's in this repo

| Folder / File | What it does |
|---|---|
| `commands/` | Slash commands — shortcuts you type in Claude Code to trigger workflows (like `/new-project` or `/starter`) |
| `skills/` | Skills — reusable techniques that teach Claude how to do specific things (design, brainstorm, build visualizations, etc.) |
| `field-guide.html` | A beginner-friendly reference page covering dev terms, tools, Claude features, and workflows |
| `index.html` | Redirects to the field guide (for the GitHub Pages URL) |

---

## Setup — start here

Follow every step in order — these instructions are written to be followed literally.

### Before you start: open the field guide

The steps below use words like "repo," "clone," "terminal," and "fork." If any of those are new to you, open the field guide now and keep it in a browser tab — it's a plain-English glossary and reference built for people who have never coded before. Whenever a term below feels unfamiliar, check there first.

1. Go to [this direct link](https://raw.githubusercontent.com/zleavitt-401/starter-repo/main/field-guide.html)
2. Your browser will either show it as plain text or ask where to save it — if it just shows text, save the page (`Cmd+S` / `Ctrl+S`) as `field-guide.html`
3. Find the saved `field-guide.html` file (likely in your Downloads folder) and double-click it — it opens in your web browser, fully formatted

> **Note:** Once you finish Setup below, your own copy will have a clean, permanent web link instead (see "Read the field guide" further down) — but you don't need to wait until then to start using it.

### Helpful Tips

- If you're ever confused, unsure, or something isn't working, just ask Claude
- Screenshots are extremely useful — if a dialogue pops up requiring a decision, take a screenshot and show Claude. It'll explain and advise
- To show Claude text on your screen, dropping a screenshot into the chat is often quicker than copy/pasting
- Every new term is also in the field guide — you don't need to memorize anything before you begin

### Step 1: Create a Claude account and a GitHub account

1. Go to [claude.ai](https://claude.ai)
2. Create an account if you don't have one
3. Subscribe to a paid plan — **Claude Pro** ($20/month) is the cheapest option and unlocks Claude Code (Max, Team, and Enterprise plans also work)
4. Go to [github.com/join](https://github.com/join) and create a free GitHub account if you don't have one — you'll use this to save your own copy of this repo and host your projects

> **Why GitHub too?** Claude writes and saves your code, but GitHub is where it lives online — it's what lets you keep a copy of this kit under your own account, publish projects, and get updates. You'll use it throughout the rest of setup.

### Step 2: Install the Claude app

The Claude app is a free download with three tabs, and each does a different job:

- **Chat** — talk with Claude like a conversation. Good for questions, brainstorming, and writing. When Claude produces something substantial here (a webpage, a document, a diagram), it opens in a side panel called an **Artifact** — you can view it live, keep iterating on it, and come back to it later.
- **Cowork** — give Claude a folder and a task, and it works semi-independently to produce finished files (a Word doc, a spreadsheet, a slide deck) — you approve its plan first, then it goes and does the work.
- **Code** — where you'll do all your building in this kit. This is Claude Code with a full interface, no separate installs required. It reads and writes real project files, runs commands in a terminal, and is what every step below uses.

This kit lives entirely in the **Code** tab — the other two are worth knowing about, but you won't need them to follow this guide. (The field guide has more on all three, plus Artifacts, if you want the fuller picture.)

1. Go to [claude.com/download](https://claude.com/download)
2. Download for your computer (macOS or Windows; Linux is available in beta)
3. Open the downloaded file and install it like any other app
4. Open the Claude app and sign in with the account you created in Step 1

> **This one app replaces what used to require VS Code + a separate extension + a Node.js install.** You don't need any of those to get started — everything happens inside the Claude app now.

> **Windows users:** Local coding sessions need [Git for Windows](https://git-scm.com/downloads/win) installed. The app checks for this itself and will prompt you if it's missing.

### Step 3: Fork and clone this repo

A "repo" (repository) is just a project folder that Git and GitHub track — this whole starter kit is one. "Forking" makes your own copy of this repo under your GitHub account. "Cloning" then downloads that copy to your computer using Git. You want your own fork (not the original) so it's yours to keep, update, and eventually host on GitHub Pages.

1. Go to [github.com/zleavitt-401/starter-repo](https://github.com/zleavitt-401/starter-repo) and sign in with the GitHub account from Step 1
2. Click **Fork** (top right of the page) → **Create fork**. This creates `github.com/<your-github-username>/starter-repo`
3. Open the Claude app and click the **Code** tab
4. Open the built-in terminal — a text-based window where you type commands instead of clicking buttons; it looks intimidating at first but you'll only ever need to copy/paste the exact lines given here (press `` Cmd+` `` on Mac / `` Ctrl+` `` on Windows, or find it in the Views menu)
5. Copy this line into the terminal, replace `<your-github-username>` with your actual GitHub username (visible in your fork's URL), then press Enter:

```
git clone https://github.com/<your-github-username>/starter-repo ~/.claude
```

> **What this does:** It downloads your fork of this repo into a hidden folder called `.claude` in your home directory. This is the exact folder where Claude Code looks for commands and skills. That's why it has to go here — if you put it somewhere else, Claude won't find it.

> **If you get an error saying the folder already exists:** You may already have a `~/.claude` folder from a previous Claude Code session. Back it up first by running `mv ~/.claude ~/.claude-backup` in the terminal, then try the clone command again. After cloning, you can copy any personal files from the backup into the new folder.

> **Windows users:** The command is slightly different. Use this instead (with your GitHub username in place of `<your-github-username>`):
> ```
> git clone https://github.com/<your-github-username>/starter-repo %USERPROFILE%\.claude
> ```

### Step 4: Open the Code tab and start a session

1. In the Claude app, click the **Code** tab (next to Chat and Cowork)
2. Choose **Local** as your environment
3. Select the `~/.claude` folder you just cloned as your project folder
4. Pick a model — **Sonnet** is a good default
5. Leave the permission mode on **Manual** for now — Claude will ask before changing anything, which is the safest way to get started

> **About permission modes:** The mode selector next to the send button controls how much Claude does without asking. **Manual** (the default) asks before every change — recommended while you're learning. Once you're comfortable, you can switch to **Accept edits** for faster iteration, or turn on **Bypass permissions** in Settings → Claude Code if you want Claude to run without stopping to ask. None of this is required to get started.

### Step 5: Run /starter

This is the last step. It finishes setting up your environment by installing a few more tools and connecting your accounts.

`/starter` is a **slash command** — a shortcut typed directly into the Claude chat that tells Claude to run a pre-written set of instructions, instead of you describing what you want in your own words. This repo comes with several (see "See all available commands" below); you'll type them the same way anytime you use one.

1. In the Code tab's chat, type `/starter` and press Enter
2. Claude will walk you through the rest — just follow its instructions. It may ask you to log into GitHub or **Vercel** in a browser window that pops up; that's expected. (Vercel is a free service that takes the app you build and publishes it to a real, public web address — `/starter` connects your account to it now so `/new-project` can use it later.)
3. This step can take a few minutes, especially if it needs to install anything — that's normal, just wait for Claude to finish each part before responding

When `/starter` finishes, Claude will show a summary confirming each tool is connected (Node, Git, GitHub, Vercel, commands, and skills all listed with checkmarks). You're ready to build. If anything shows an error instead of a checkmark, tell Claude and it'll help you fix it before moving on.

---

## Optional: Set up VS Code too

You don't need this. The Claude app's Code tab covers everything in this kit. But if you'd like a dedicated code editor to browse and read your files in — nice for peeking at what Claude built, or if you outgrow this kit later — you can add VS Code any time.

1. Go to [code.visualstudio.com](https://code.visualstudio.com) and install it like any other app
2. From a Code tab session in the Claude app, look for **Continue in...** — it hands your current session off to VS Code with the same files and context, no separate setup needed
3. If you'd rather run Claude Code as a standalone VS Code extension instead, search **Claude Code** in the Extensions sidebar (`Cmd+Shift+X` / `Ctrl+Shift+X`) and install the one by **Anthropic** — it shares the same `~/.claude` config, so nothing here needs to be redone

If you do set up VS Code, these extensions used to be recommended alongside it (the Claude app's Code tab already includes their equivalents natively, so they're just for VS Code itself):

- **GitLens** — shows who changed what in your code and when
- **Prettier** — automatically makes your code look clean when you save
- **Live Server** — lets you preview HTML files in your browser with live reloading
- **Error Lens** — shows error messages right next to the problem line in your code

---

## After setup

### Start your first project

Type `/new-project` in Claude Code. It will ask you what to name your project, then create a new app folder, set up a GitHub repo, and connect it to Vercel (which publishes your app to the internet) — all automatically. Expect it to ask a couple of questions and take a minute or two; when it's done it'll give you a project folder, a GitHub link, and confirmation that everything's connected.

### See all available commands

Type `/` in Claude Code to see every command available. The most important ones:

- `/new-project` — start a new app
- **Spec Kit** — a structured workflow for planning and building features with Claude — use `/constitution` → `/specify` → `/plan` → `/implement`
- `/update-docs` — update your project's documentation after making changes

### Using skills in claude.ai chat (not just Claude Code)

The skills in this kit (see `skills/` below) run automatically in **Claude Code** — you never have to think about them there. But if you also want to use skills like brainstorming or prompt-generation in regular **claude.ai chat** (in a browser, not Claude Code), they don't carry over automatically — chat and Claude Code are separate, so each skill has to be uploaded once, per account:

1. In claude.ai, go to **Settings → Capabilities** and make sure "code execution and file creation" is turned on
2. Go to **Settings → Capabilities → Skills**, click **+**, then **Create skill → Upload a skill**
3. In `~/.claude/skills/`, find the skill folder you want (e.g. `brainstorming-ideas-into-designs`), zip that folder, and upload the zip
4. The skill now appears in your claude.ai skills list and can be toggled on for any chat

This is private to your account and only needs to be done once per skill. Note that a couple of skills in this kit (like `implementation-prompt-generator`) are written to hand off into Claude Code slash commands like `/speckit.specify` — those hand-off steps only work inside Claude Code, so in chat you'd copy the generated prompt over to Claude Code yourself.

### Read the field guide

Open the field guide for a beginner-friendly reference covering dev terms, tools, and workflows:

**`<your-github-username>.github.io/starter-repo`**

(Replace `<your-github-username>` with your own GitHub username. This link works after you enable GitHub Pages on your fork — see below.)

---

## Getting updates

When new commands or skills are added to this repo, you can get them with one command:

1. Open the Claude app's Code tab
2. Open the integrated terminal (`` Cmd+` `` / `` Ctrl+` ``) — or your VS Code terminal, if that's what you're using
3. Run:

```
cd ~/.claude && git pull
```

That's it. New commands and skills will be available immediately in Claude Code.

> **If git pull gives an error about "divergent branches":** Run `cd ~/.claude && git pull --rebase` instead. This happens rarely and is harmless.

> **Important:** Don't edit the files that came with this repo (commands, skills, etc.). If you change a repo file and then run `git pull`, Git may ask you to resolve a conflict — which is confusing. Instead, create your own new files (see below).

---

## Adding your own skills

You can create your own skills without conflicting with this repo:

1. Create a new folder inside `~/.claude/skills/` with any name you want
2. Add a `SKILL.md` file inside it — this is what Claude reads to learn the skill
3. Your folder will show as "untracked" in Git, which means `git pull` will never touch it

Your personal skills and the repo skills live side by side. Updates to the repo won't affect anything you've added.

---

## Enabling GitHub Pages (for the field guide URL)

This is a one-time step to make the field guide available as a website:

1. Go to your fork on GitHub (github.com/`<your-github-username>`/starter-repo)
2. Click **Settings** (tab at the top of the repo page)
3. In the left sidebar, click **Pages**
4. Under "Source," select **Deploy from a branch**
5. Under "Branch," select **main** and leave the folder as **/ (root)**
6. Click **Save**
7. Wait a minute or two — your field guide will be live at `<your-github-username>.github.io/starter-repo`

Bookmark that link — it's now your permanent, always-up-to-date field guide.

---

## What's here (for the curious)

```
~/.claude/
├── commands/          ← Slash commands (type / in Claude Code to use them)
│   ├── starter.md
│   ├── new-project.md
│   ├── continue.md
│   ├── update-docs.md
│   ├── update-claude-md.md
│   ├── speckit.constitution.md
│   ├── speckit.specify.md
│   ├── speckit.clarify.md
│   ├── speckit.plan.md
│   ├── speckit.tasks.md
│   ├── speckit.analyze.md
│   ├── speckit.implement.md
│   └── ...
├── skills/            ← Skills (Claude loads these automatically)
│   ├── frontend-design/
│   ├── brainstorming-ideas-into-designs/
│   ├── implementation-prompt-generator/
│   ├── skill-converter/
│   ├── rules-generator/
│   ├── ui-ux-pro-max/
│   ├── d3-viz/
│   └── (your own skills go here too)
├── field-guide.html   ← Beginner reference page
├── index.html         ← Redirects to the field guide
└── README.md          ← This file
```
