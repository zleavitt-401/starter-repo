# Feature Specification: Starter Repo Kit

**Feature Branch**: `001-starter-kit`
**Created**: 2026-03-16
**Status**: Draft
**Input**: User description: "Build the starter-repo GitHub starter kit for sharing with non-technical friends who want to learn development using Claude."

## User Scenarios & Testing *(mandatory)*

### User Story 1 — First-Time Setup (Priority: P1)

A complete beginner receives a GitHub link from a friend. They have never
written code, used a terminal, or installed developer tools. They read the
README on github.com, follow every step in order, and end up with a fully
configured Claude development environment — VS Code open, Claude Code
extension active, all skills loaded, all slash commands available, and
developer tools (GitHub CLI, Vercel CLI) connected.

**Why this priority**: This is the entire reason the repo exists. If a
beginner cannot follow the README to a working setup, nothing else matters.

**Independent Test**: A person with no coding experience reads the README on
GitHub, follows every step from top to bottom on a fresh Mac, and ends with
`/starter` completing successfully and all commands visible when typing `/`
in Claude Code.

**Acceptance Scenarios**:

1. **Given** a fresh macOS computer with no developer tools installed,
   **When** the user follows README steps 1–8 in order,
   **Then** they have VS Code open with Claude Code signed in, the repo
   cloned to `~/.claude`, and `/starter` completes with all checks passing.

2. **Given** the user has completed all README steps,
   **When** they type `/` in the Claude Code panel,
   **Then** they see all included slash commands (starter, new-project,
   constitution, specify, clarify, plan, tasks, analyze, implement,
   update-docs, update-claude-md, continue).

3. **Given** the user has completed setup,
   **When** Claude Code loads in any project folder,
   **Then** all included skills (frontend-design, brainstorming-ideas-into-designs,
   implementation-prompt-generator, skill-converter, rules-generator,
   ui-ux-pro-max, d3-viz) are available to Claude.

---

### User Story 2 — Receiving Updates (Priority: P2)

After initial setup, the repo maintainer adds new commands or skills and
pushes them to GitHub. The recipient opens their terminal, runs `git pull`
from `~/.claude`, and immediately has access to the new content without
reinstalling anything or losing any personal files.

**Why this priority**: The repo is meant to be a living kit that grows over
time. If updates break the setup or require manual intervention, the
recipient will stop updating.

**Independent Test**: After initial setup is complete, a new command file is
added to the remote repo. The user runs `cd ~/.claude && git pull` and the
new command appears when typing `/` in Claude Code.

**Acceptance Scenarios**:

1. **Given** a user with a working setup from Story 1,
   **When** the maintainer pushes a new command to the repo and the user
   runs `git pull` from `~/.claude`,
   **Then** the new command appears in Claude Code without any additional
   steps.

2. **Given** a user with a working setup,
   **When** the maintainer pushes an updated skill and the user runs
   `git pull`,
   **Then** the updated skill content is available in Claude Code
   immediately.

---

### User Story 3 — Adding Personal Skills (Priority: P3)

A user who has completed setup creates their own skill folder inside
`~/.claude/skills/` with a custom SKILL.md. Their personal skill works in
Claude Code alongside the repo-provided skills. When they run `git pull`,
their personal skill is not touched, deleted, or conflicted.

**Why this priority**: Users MUST be able to extend their setup without
fear of losing personal work. This is essential for long-term adoption but
depends on Stories 1 and 2 working first.

**Independent Test**: Create a folder `~/.claude/skills/my-custom-skill/`
with a SKILL.md file. Run `git pull`. Verify the personal skill folder is
unchanged and `git status` shows it as untracked.

**Acceptance Scenarios**:

1. **Given** a user with a working setup who has created
   `~/.claude/skills/my-custom-skill/SKILL.md`,
   **When** they run `git pull` from `~/.claude`,
   **Then** their personal skill folder is untouched and still works in
   Claude Code.

2. **Given** a user with personal skills,
   **When** they run `git status` from `~/.claude`,
   **Then** their personal skill folders appear as "untracked" and are not
   staged or committed.

---

### Edge Cases

- What happens when `~/.claude` already exists from a prior Claude Code
  installation? The clone command will fail. README MUST explain how to
  handle this (back up existing folder, or merge manually).
- What happens when the user has no Homebrew installed? The `/starter`
  command MUST detect this and install Homebrew before proceeding with
  `brew install gh`.
- What happens when `git pull` encounters a merge conflict because the
  user edited a repo-provided file? README MUST advise users to only add
  new files, never edit existing repo files. `/starter` command MUST
  handle this gracefully with a clear error message.
- What happens on Windows? README MUST note the different clone path
  (`%USERPROFILE%\.claude`) and `/starter` MUST support `winget` as an
  alternative to `brew` for installing GitHub CLI.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: README MUST guide a complete beginner through setup using
  only numbered steps and plain English — no jargon without explanation
- **FR-002**: README MUST cover creating a Claude Pro account, installing
  VS Code, installing Node.js LTS, cloning the repo to `~/.claude`,
  installing the Claude Code extension, enabling Bypass Permissions, and
  installing recommended extensions (GitLens, Prettier, Live Server,
  Error Lens)
- **FR-003**: README MUST include the GitHub Pages URL for the field guide
- **FR-004**: README MUST explain how to receive updates via `git pull`
- **FR-005**: README MUST explain how to add personal skills without
  conflicting with repo files
- **FR-006**: `/starter` command MUST run `git pull` as its first step to
  ensure the latest files are present
- **FR-007**: `/starter` command MUST verify Node.js is installed, install
  GitHub CLI (brew on Mac, winget on Windows), run `gh auth login`, set
  Git identity (prompt for name and email), install Vercel CLI, run
  `vercel login`, and display a final verification summary
- **FR-008**: The `skills/` folder MUST contain these skills as exact
  copies: frontend-design, brainstorming-ideas-into-designs,
  implementation-prompt-generator, skill-converter, rules-generator,
  ui-ux-pro-max, d3-viz
- **FR-009**: The `commands/` folder MUST contain: all speckit commands
  (constitution, specify, clarify, plan, tasks, analyze, implement),
  continue, update-docs, update-claude-md, new-project, and starter
- **FR-010**: `field-guide.html` MUST be a self-contained HTML file with
  no external dependencies beyond Google Fonts CDN
- **FR-011**: `index.html` MUST redirect to `field-guide.html` for GitHub
  Pages compatibility
- **FR-012**: All file paths MUST assume macOS as the primary platform with
  Windows differences noted where relevant
- **FR-013**: The repo MUST contain no package.json, no node_modules, no
  build step, and no application framework code

### Key Entities

- **README.md**: The entry point — a sequential setup guide that a complete
  beginner reads on github.com and follows step by step
- **commands/**: Folder of `.md` files, each defining a slash command that
  Claude Code discovers automatically from `~/.claude/commands/`
- **skills/**: Folder of subfolders, each containing a `SKILL.md` that
  Claude Code discovers automatically from `~/.claude/skills/`
- **field-guide.html**: A self-contained HTML reference page covering dev
  terms, tools, Claude features, and workflows
- **index.html**: A redirect page for GitHub Pages that sends visitors to
  the field guide

## Scope

**In scope**: README, /starter command, skills folder, commands folder,
field-guide.html, index.html redirect, GitHub Pages configuration
instructions

**Out of scope**: Application code, package.json, CI/CD pipelines,
automated testing, Windows-only optimization

## Assumptions

- User is on macOS with Homebrew available or installable
- User has a paid Claude Pro account before starting
- Repo is hosted at github.com/zleavitt-401/starter-repo
- GitHub Pages will be enabled manually in repo settings after first push
- Two skills (md-generator, debugging-lightweight-stacks) are not yet
  available on the source machine and will be added in a future update

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A person who has never written code can follow the README and
  reach a working Claude Code setup in under 30 minutes
- **SC-002**: After setup, 100% of included slash commands appear when
  typing `/` in Claude Code
- **SC-003**: After setup, all included skills are available to Claude Code
  across any project folder
- **SC-004**: Running `git pull` from `~/.claude` updates repo content
  without prompting for merge resolution or touching user-added files
- **SC-005**: `field-guide.html` renders correctly when opened locally in a
  browser and when served via GitHub Pages
- **SC-006**: The `/starter` command completes all steps without errors on a
  fresh macOS machine with Node.js pre-installed
