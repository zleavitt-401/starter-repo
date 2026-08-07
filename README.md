# Starter Repo

Everything you need to start building with Claude — commands, skills, and a field guide — in one place.

This repo is designed to be cloned once to a special folder on your computer. After that, Claude — in the Claude app's **Code** tab — will have access to all the tools and shortcuts included here. No coding experience required.

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

### Helpful Tips

- If you're ever confused, unsure, or something isn't working, just ask Claude
- Screenshots are extremely useful — if a dialogue pops up requiring a decision, take a screenshot and show Claude. It'll explain and advise
- To show Claude text on your screen, dropping a screenshot into the chat is often quicker than copy/pasting

### Step 1: Create a Claude account

1. Go to [claude.ai](https://claude.ai)
2. Create an account if you don't have one
3. Subscribe to a paid plan — **Claude Pro** ($20/month) is the cheapest option and unlocks Claude Code (Max, Team, and Enterprise plans also work)

### Step 2: Install the Claude app

The Claude app is a free download with three tabs — **Chat**, **Cowork**, and **Code**. The **Code** tab is where you'll do all your building — it's Claude Code with a full interface, no separate installs required.

1. Go to [claude.com/download](https://claude.com/download)
2. Download for your computer (macOS or Windows; Linux is available in beta)
3. Open the downloaded file and install it like any other app
4. Open the Claude app and sign in with the account you created in Step 1

> **This one app replaces what used to require VS Code + a separate extension + a Node.js install.** You don't need any of those to get started — everything happens inside the Claude app now.

> **Windows users:** Local coding sessions need [Git for Windows](https://git-scm.com/downloads/win) installed. The app checks for this itself and will prompt you if it's missing.

### Step 3: Clone this repo

"Cloning" means downloading a copy of this folder to your computer using Git.

1. Open the Claude app and click the **Code** tab
2. Open the built-in terminal (press `` Cmd+` `` on Mac / `` Ctrl+` `` on Windows, or find it in the Views menu)
3. Copy and paste this entire line into the terminal, then press Enter:

```
git clone https://github.com/zleavitt-401/starter-repo ~/.claude
```

> **What this does:** It downloads this entire repo into a hidden folder called `.claude` in your home directory. This is the exact folder where Claude Code looks for commands and skills. That's why it has to go here — if you put it somewhere else, Claude won't find it.

> **If you get an error saying the folder already exists:** You may already have a `~/.claude` folder from a previous Claude Code session. Back it up first by running `mv ~/.claude ~/.claude-backup` in the terminal, then try the clone command again. After cloning, you can copy any personal files from the backup into the new folder.

> **Windows users:** The command is slightly different. Use this instead:
> ```
> git clone https://github.com/zleavitt-401/starter-repo %USERPROFILE%\.claude
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

1. In the Code tab's chat, type `/starter` and press Enter
2. Claude will walk you through the rest — just follow its instructions

When `/starter` finishes, you'll see a summary showing everything is connected. You're ready to build.

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

Type `/new-project` in Claude Code. It will create a new app folder, set up GitHub, and connect it to Vercel (which publishes your app to the internet) — all automatically.

### See all available commands

Type `/` in Claude Code to see every command available. The most important ones:

- `/new-project` — start a new app
- **Spec Kit** — a structured workflow for planning and building features with Claude — use `/constitution` → `/specify` → `/plan` → `/implement`
- `/update-docs` — update your project's documentation after making changes

### Read the field guide

Open the field guide for a beginner-friendly reference covering dev terms, tools, and workflows:

**[zleavitt-401.github.io/starter-repo](https://zleavitt-401.github.io/starter-repo)**

(This link works after you enable GitHub Pages — see below.)

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

1. Go to your repo on GitHub (github.com/zleavitt-401/starter-repo)
2. Click **Settings** (tab at the top of the repo page)
3. In the left sidebar, click **Pages**
4. Under "Source," select **Deploy from a branch**
5. Under "Branch," select **main** and leave the folder as **/ (root)**
6. Click **Save**
7. Wait a minute or two — your field guide will be live at `zleavitt-401.github.io/starter-repo`

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
