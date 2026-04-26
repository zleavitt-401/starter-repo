# Starter Repo

Everything you need to start building with Claude — commands, skills, and a field guide — in one place.

This repo is designed to be cloned once to a special folder on your computer. After that, Claude Code (inside VS Code) will have access to all the tools and shortcuts included here. No coding experience required.

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
3. Subscribe to **Claude Pro** ($20/month) — this is required for Claude Code to work

### Step 2: Install VS Code

VS Code is an IDE (Integrated Development Environment) — a free app where you write and manage code, and talk to Claude.

1. Go to [code.visualstudio.com](https://code.visualstudio.com)
2. Click the big download button — it will detect your computer type automatically
3. Open the downloaded file and drag VS Code to your Applications folder (Mac) or run the installer (Windows)
4. Open VS Code

### Step 3: Install Node.js

Node.js is a tool that runs behind the scenes. Claude Code and other developer tools need it.

1. Go to [nodejs.org](https://nodejs.org)
2. Download the **LTS** version (the one on the left — LTS means "Long Term Support," which just means "the stable one")
3. Open the downloaded file and follow the installer
4. When it's done, **restart VS Code** (close it and open it again)

### Step 4: Clone this repo

"Cloning" means downloading a copy of this folder to your computer using Git (which was installed with Node.js).

1. Open VS Code
2. Open the built-in terminal: click **Terminal** in the top menu bar, then **New Terminal**
3. A panel will appear at the bottom of VS Code — this is the terminal
4. Copy and paste this entire line into the terminal, then press Enter:

```
git clone https://github.com/zleavitt-401/starter-repo ~/.claude
```

> **What this does:** It downloads this entire repo into a hidden folder called `.claude` in your home directory. This is the exact folder where Claude Code looks for commands and skills. That's why it has to go here — if you put it somewhere else, Claude won't find it.

> **If you get an error saying the folder already exists:** You may already have a `~/.claude` folder from a previous Claude Code session. Back it up first by running `mv ~/.claude ~/.claude-backup` in the terminal, then try the clone command again. After cloning, you can copy any personal files from the backup into the new folder.

> **Windows users:** The command is slightly different. Use this instead:
> ```
> git clone https://github.com/zleavitt-401/starter-repo %USERPROFILE%\.claude
> ```

### Step 5: Install the Claude Code extension

1. In VS Code, click the **Extensions** icon in the left sidebar (it looks like four squares)
   - Or press `Cmd+Shift+X` on Mac / `Ctrl+Shift+X` on Windows
2. Search for **Claude Code**
3. Find the one by **Anthropic** and click **Install**
4. After it installs, you'll see a Claude icon in your left sidebar — click it to open the Claude panel
5. Sign in with the same account you created in Step 1

### Step 6: Enable Bypass Permissions

This setting lets Claude Code run commands without asking for permission every single time. It makes the experience much smoother.

1. Open VS Code Settings: press `Cmd+,` on Mac / `Ctrl+,` on Windows
2. Search for **Claude Code bypass**
3. Find the setting called **Bypass Permissions** and check the box to enable it

> **Is this safe?** Yes, for learning and personal projects. Claude will still tell you what it's doing — it just won't pause and wait for you to click "Allow" on every single action.

### Step 7: Install recommended extensions

These are optional but make your life much easier. Install them the same way you installed Claude Code (Extensions sidebar → search → Install):

- **GitLens** — shows who changed what in your code and when
- **Prettier** — automatically makes your code look clean when you save
- **Live Server** — lets you preview HTML files in your browser with live reloading
- **Error Lens** — shows error messages right next to the problem line in your code

### Step 8: Run /starter

This is the last step. It finishes setting up your environment by installing a few more tools and connecting your accounts.

1. Click the Claude icon in the left sidebar to open the Claude panel
2. Type `/starter` and press Enter
3. Claude will walk you through the rest — just follow its instructions

When `/starter` finishes, you'll see a summary showing everything is connected. You're ready to build.

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

1. Open VS Code
2. Open the terminal (`Terminal` → `New Terminal`)
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
