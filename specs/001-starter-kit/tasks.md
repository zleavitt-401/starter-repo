# Tasks: Starter Repo Kit

**Input**: Design documents from `/specs/001-starter-kit/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md

**Tests**: Not requested in the feature specification. No test tasks included.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Initialize repo structure and copy source files

- [x] T001 Create `commands/` directory at repo root
- [x] T002 Create `skills/` directory at repo root
- [x] T003 [P] Create `.gitignore` at repo root excluding `.DS_Store`, `memory/`, `__pycache__/`, editor swap files

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Copy all commands and skills from the maintainer's machine. These files MUST be in place before any user story can be validated.

**Commands** (copy from `~/.claude/commands/`):

- [x] T004 [P] Copy `commands/starter.md` from `~/.claude/commands/starter.md` (will be updated in US1 phase)
- [x] T005 [P] Copy `commands/new-project.md` from `~/.claude/commands/new-project.md`
- [x] T006 [P] Copy `commands/continue.md` from `~/.claude/commands/continue.md`
- [x] T007 [P] Copy `commands/update-docs.md` from `~/.claude/commands/update-docs.md`
- [x] T008 [P] Copy `commands/update-claude-md.md` from `~/.claude/commands/update-claude-md.md`
- [x] T009 [P] Copy `commands/frontend-design.md` from `~/.claude/commands/frontend-design.md`
- [x] T010 [P] Copy `commands/handoff.md` from `~/.claude/commands/handoff.md`
- [x] T011 [P] Copy `commands/speckit.constitution.md` from `~/.claude/commands/speckit.constitution.md`
- [x] T012 [P] Copy `commands/speckit.specify.md` from `~/.claude/commands/speckit.specify.md`
- [x] T013 [P] Copy `commands/speckit.clarify.md` from `~/.claude/commands/speckit.clarify.md`
- [x] T014 [P] Copy `commands/speckit.plan.md` from `~/.claude/commands/speckit.plan.md`
- [x] T015 [P] Copy `commands/speckit.tasks.md` from `~/.claude/commands/speckit.tasks.md`
- [x] T016 [P] Copy `commands/speckit.analyze.md` from `~/.claude/commands/speckit.analyze.md`
- [x] T017 [P] Copy `commands/speckit.implement.md` from `~/.claude/commands/speckit.implement.md`
- [x] T018 [P] Copy `commands/speckit.checklist.md` from `~/.claude/commands/speckit.checklist.md`
- [x] T019 [P] Copy `commands/speckit.taskstoissues.md` from `~/.claude/commands/speckit.taskstoissues.md`

**Skills** (copy from `~/.claude/skills/`):

- [x] T020 [P] Copy `skills/frontend-design/` from `~/.claude/skills/frontend-design/` (recursive)
- [x] T021 [P] Copy `skills/brainstorming-ideas-into-designs/` — source: maintainer's Downloads or skills archive
- [x] T022 [P] Copy `skills/implementation-prompt-generator/` — source: maintainer's Downloads or skills archive
- [x] T023 [P] Copy `skills/skill-converter/` from `~/.claude/skills/skill-converter/` (recursive)
- [x] T024 [P] Copy `skills/rules-generator/` — source: maintainer's Downloads or skills archive
- [x] T025 [P] Copy `skills/ui-ux-pro-max/` from `~/.claude/skills/ui-ux-pro-max/` (recursive)
- [x] T026 [P] Copy `skills/d3-viz/` from `~/.claude/skills/d3-viz/` (recursive)

**Checkpoint**: All commands and skills are in place. User story work can begin.

---

## Phase 3: User Story 1 — First-Time Setup (Priority: P1) 🎯 MVP

**Goal**: A complete beginner follows the README and ends with a fully configured Claude development environment.

**Independent Test**: A person with no coding experience reads the README on GitHub, follows every step, and ends with `/starter` completing successfully and all commands visible when typing `/` in Claude Code.

### Implementation for User Story 1

- [x] T027 [US1] Write `README.md` at repo root — beginner setup guide with steps 1–8 covering: Claude Pro account, VS Code install, Node.js LTS install, git clone to `~/.claude`, Claude Code extension + Bypass Permissions, recommended extensions (GitLens, Prettier, Live Server, Error Lens), running `/starter` (FR-001, FR-002)
- [x] T028 [US1] Add GitHub Pages field guide URL to README.md in the "After setup" section (FR-003)
- [x] T029 [US1] Add "Getting updates" section to README.md explaining `cd ~/.claude && git pull` (FR-004)
- [x] T030 [US1] Add "Adding your own skills" section to README.md explaining untracked folders survive git pull (FR-005)
- [x] T031 [US1] Add "What's here" section to README.md with directory tree showing all commands and skills
- [x] T032 [US1] Add edge case guidance to README.md: handling existing `~/.claude` folder (back up first), Windows clone path (`%USERPROFILE%\.claude`)
- [x] T033 [US1] Update `commands/starter.md` for Option C flow: add `git pull` as Step 1, remove repo-cloning step, add Homebrew detection and install, keep Node.js check / GitHub CLI / gh auth / Git identity / Vercel CLI / vercel login / final summary (FR-006, FR-007)
- [x] T034 [P] [US1] Create `field-guide.html` at repo root — copy self-contained HTML file with inline CSS/JS and Google Fonts CDN only (FR-010)
- [x] T035 [P] [US1] Create `index.html` at repo root — meta refresh redirect to `field-guide.html` (FR-011)
- [x] T036 [US1] Add GitHub Pages setup instructions to README.md (Settings → Pages → Deploy from branch → main → root)

**Checkpoint**: At this point, a beginner can follow the README end-to-end and have a working setup. All commands visible via `/`, all skills loaded, field guide accessible.

---

## Phase 4: User Story 2 — Receiving Updates (Priority: P2)

**Goal**: Running `git pull` from `~/.claude` brings new commands and skills without breaking anything.

**Independent Test**: Push a new command to the remote repo, run `git pull` from `~/.claude`, verify the new command appears in Claude Code.

### Implementation for User Story 2

- [x] T037 [US2] Verify `.gitignore` excludes `memory/`, `.DS_Store`, and `__pycache__/` so git pull never touches user-generated files in `.gitignore`
- [x] T038 [US2] Verify `commands/starter.md` Step 1 runs `git pull` before doing anything else, so the latest files are always pulled at setup time (FR-006)
- [x] T039 [US2] Add `git pull` troubleshooting to README.md: divergent branches → use `git pull --rebase`; merge conflict → advise not editing repo files

**Checkpoint**: git pull updates repo content cleanly. No merge prompts for standard usage.

---

## Phase 5: User Story 3 — Adding Personal Skills (Priority: P3)

**Goal**: Users can create personal skill folders that coexist with repo skills and survive git pull.

**Independent Test**: Create `~/.claude/skills/my-custom-skill/SKILL.md`, run `git pull`, verify folder is untouched and shows as untracked in `git status`.

### Implementation for User Story 3

- [x] T040 [US3] Verify `.gitignore` does NOT include `skills/` — personal skill folders must remain untracked (not ignored), so they show in `git status` but are never committed
- [x] T041 [US3] Verify README.md "Adding your own skills" section explains: create folder in `~/.claude/skills/`, add SKILL.md, folder stays untracked, git pull never touches it

**Checkpoint**: Personal skills coexist safely. Users can extend without fear.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and cleanup

- [x] T042 Verify repo contains NO package.json, node_modules, or build configuration files (FR-013)
- [x] T043 Verify all file paths in README.md use macOS conventions with Windows alternatives noted (FR-012)
- [x] T044 Verify `field-guide.html` renders correctly when opened as a local file and when served via GitHub Pages
- [x] T045 Review all markdown files for plain English — no unexplained jargon, every term defined on first use
- [x] T046 Verify all command `.md` files have `description` in YAML frontmatter
- [x] T047 Verify all skill folders contain a `SKILL.md` file
- [x] T048 Run final file inventory: confirm command count matches FR-009 list, skill count matches FR-008 list

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — can start immediately
- **Foundational (Phase 2)**: Depends on Phase 1 (directories exist) — BLOCKS all user stories
- **User Story 1 (Phase 3)**: Depends on Phase 2 (all commands and skills copied)
- **User Story 2 (Phase 4)**: Depends on Phase 3 (README and starter exist to verify)
- **User Story 3 (Phase 5)**: Depends on Phase 3 (README exists to verify)
- **Polish (Phase 6)**: Depends on all user stories complete

### User Story Dependencies

- **User Story 1 (P1)**: Depends on Foundational — no dependencies on other stories
- **User Story 2 (P2)**: Depends on US1 completion (needs README and starter to verify git pull behavior)
- **User Story 3 (P3)**: Depends on US1 completion (needs README to verify personal skills section)

### Within Each User Story

- README sections before verification tasks
- Starter command update before verification
- File creation before cross-referencing

### Parallel Opportunities

- All Phase 1 setup tasks (T001–T003) can run in parallel
- All Phase 2 command copies (T004–T019) can run in parallel
- All Phase 2 skill copies (T020–T026) can run in parallel
- T034 and T035 (field-guide.html and index.html) can run in parallel with README writing
- US2 and US3 phases can run in parallel after US1 completes

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (create directories)
2. Complete Phase 2: Foundational (copy all commands and skills)
3. Complete Phase 3: User Story 1 (README, starter update, field guide, index.html)
4. **STOP and VALIDATE**: Have a beginner test the full flow on a fresh Mac
5. Deploy: push to GitHub, enable GitHub Pages

### Incremental Delivery

1. Setup + Foundational → files in place
2. User Story 1 → beginner can follow README to working setup (MVP!)
3. User Story 2 → git pull verified as safe update mechanism
4. User Story 3 → personal skills verified as safe to add
5. Polish → final quality pass

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Most files already exist from prior work in this session — tasks should verify and update rather than create from scratch where applicable
- Two skills (md-generator, debugging-lightweight-stacks) are deferred — not available on source machine
- Commit after each phase completion
