# Implementation Plan: Starter Repo Kit

**Branch**: `001-starter-kit` | **Date**: 2026-03-16 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-starter-kit/spec.md`

## Summary

Build a shareable GitHub starter kit containing Claude Code commands, skills,
a field guide HTML page, and a beginner-friendly README. The repo is a static
file collection — no application code, no build tools, no framework. Files are
copied from the maintainer's machine and organized into the `~/.claude`
directory structure so recipients can clone once and have a fully configured
Claude development environment.

## Technical Context

**Language/Version**: Markdown, HTML5 (no build step, no transpilation)
**Primary Dependencies**: None (Google Fonts CDN is the only external resource)
**Storage**: N/A — static files only, no database
**Testing**: Manual verification (beginner follows README on fresh Mac)
**Target Platform**: macOS (primary), Windows (secondary, noted where different)
**Project Type**: Static file kit / documentation repository
**Performance Goals**: N/A — no runtime, no server
**Constraints**: No package.json, no node_modules, no build step, no CI/CD
**Scale/Scope**: Single repo, ~20 files, intended for small group of friends

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Evidence |
|-----------|--------|----------|
| I. Plain English First | PASS | README uses numbered steps, explains every term, zero jargon |
| II. Static and Simple | PASS | No package.json, no build step, no framework — vanilla files only |
| III. Clone-Ready Structure | PASS | All paths match `~/.claude/commands/` and `~/.claude/skills/` |
| IV. Human-Readable Files | PASS | No minification, HTML self-contained, markdown clean |

All gates pass. No violations to justify.

## Project Structure

### Documentation (this feature)

```text
specs/001-starter-kit/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
└── tasks.md             # Phase 2 output (/speckit.tasks command)
```

### Source Code (repository root)

```text
starter-repo/
├── README.md                    # Beginner setup guide (FR-001 through FR-005)
├── index.html                   # GitHub Pages redirect to field guide (FR-011)
├── field-guide.html             # Self-contained reference page (FR-010)
├── .gitignore                   # Excludes .DS_Store, memory/, __pycache__
├── commands/                    # Slash commands for Claude Code (FR-009)
│   ├── starter.md               # Environment setup command (FR-006, FR-007)
│   ├── new-project.md
│   ├── continue.md
│   ├── update-docs.md
│   ├── update-claude-md.md
│   ├── frontend-design.md
│   ├── handoff.md
│   ├── speckit.constitution.md
│   ├── speckit.specify.md
│   ├── speckit.clarify.md
│   ├── speckit.plan.md
│   ├── speckit.tasks.md
│   ├── speckit.analyze.md
│   ├── speckit.implement.md
│   ├── speckit.checklist.md
│   └── speckit.taskstoissues.md
└── skills/                      # Skill folders for Claude Code (FR-008)
    ├── frontend-design/
    ├── brainstorming-ideas-into-designs/
    ├── implementation-prompt-generator/
    ├── skill-converter/
    ├── rules-generator/
    ├── ui-ux-pro-max/
    └── d3-viz/
```

**Structure Decision**: Flat static file layout at repository root. No src/,
no tests/, no build directories. Commands and skills are organized into their
respective folders matching Claude Code's `~/.claude` discovery paths.

## Complexity Tracking

No violations. All content is static files with no abstractions or patterns.
