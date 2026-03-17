# Research: Starter Repo Kit

**Branch**: `001-starter-kit` | **Date**: 2026-03-16

## Research Summary

This is a static file kit with no runtime dependencies, no build tools, and
no application code. Research scope is limited to file organization and
Claude Code discovery mechanics.

## Decisions

### D1: Clone destination path

**Decision**: `~/.claude` (macOS), `%USERPROFILE%\.claude` (Windows)
**Rationale**: Claude Code automatically discovers commands from
`~/.claude/commands/` and skills from `~/.claude/skills/`. Cloning the repo
directly to this path ensures zero-configuration discovery.
**Alternatives considered**: Cloning to Desktop and symlinking — rejected
because it adds complexity for beginners with no benefit.

### D2: GitHub Pages redirect strategy

**Decision**: Simple `index.html` with `<meta http-equiv="refresh">` redirect
to `field-guide.html`.
**Rationale**: No JavaScript required, works in all browsers, no build step
needed. The redirect makes the GitHub Pages root URL useful immediately.
**Alternatives considered**: Jekyll-based GitHub Pages — rejected because it
requires a build step and `_config.yml`, violating the Static and Simple
principle.

### D3: Existing ~/.claude handling

**Decision**: README warns users and provides instructions to back up any
existing `~/.claude` folder before cloning. The `/starter` command detects
if the directory is not a git repo and advises re-cloning.
**Rationale**: A beginner may have used Claude Code before receiving this
kit, creating a `~/.claude` folder with personal memory files. Overwriting
without warning would lose their data.
**Alternatives considered**: Auto-merge script — rejected because merge
logic is complex and error-prone for beginners.

### D4: Homebrew dependency

**Decision**: `/starter` command checks for Homebrew and installs it if
missing before proceeding with `brew install gh`.
**Rationale**: GitHub CLI is most reliably installed via Homebrew on macOS.
Most developer tooling assumes Homebrew is available. Installing it as part
of `/starter` removes a prerequisite the user would otherwise need to handle
manually.
**Alternatives considered**: Direct `.pkg` installer for GitHub CLI —
rejected because Homebrew is needed for other tools and is standard practice.

### D5: Update mechanism

**Decision**: `git pull` from `~/.claude`. No scripts, no installer.
**Rationale**: Git pull is the simplest possible update mechanism. New files
appear, updated files are replaced, and untracked personal files are never
touched. This requires zero tooling beyond Git (which is already installed).
**Alternatives considered**: Custom update script — rejected as unnecessary
complexity for a static file repo.

## No Unresolved Items

All technical context fields are resolved. No NEEDS CLARIFICATION markers
remain.
