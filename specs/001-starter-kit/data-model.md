# Data Model: Starter Repo Kit

**Branch**: `001-starter-kit` | **Date**: 2026-03-16

## Overview

This project has no database, no runtime state, and no application data model.
All "entities" are static files on disk discovered by Claude Code at load time.

## File Entities

### Command (commands/*.md)

A markdown file with YAML frontmatter that Claude Code discovers as a slash
command.

| Attribute | Description |
|-----------|-------------|
| filename | The command name (e.g., `starter.md` → `/starter`) |
| description | YAML frontmatter field shown in command picker |
| body | Markdown instructions Claude follows when command is invoked |

**Discovery**: Claude Code scans `~/.claude/commands/` for `.md` files at
startup and on focus.

### Skill (skills/*/SKILL.md)

A folder containing a `SKILL.md` file that Claude Code discovers as a
reusable skill.

| Attribute | Description |
|-----------|-------------|
| folder name | Human-readable skill identifier |
| SKILL.md | Instructions Claude reads to learn the skill |
| assets/ | Optional supporting files (examples, references, data) |

**Discovery**: Claude Code scans `~/.claude/skills/` for subdirectories
containing `SKILL.md` at startup and on focus.

### Field Guide (field-guide.html)

A single self-contained HTML file with inline CSS and JavaScript.

| Attribute | Description |
|-----------|-------------|
| content | Tabbed reference covering dev terms, tools, Claude features |
| dependencies | Google Fonts CDN only |
| hosting | GitHub Pages (static) or local file:// |

### README (README.md)

The repo entry point read on github.com.

| Attribute | Description |
|-----------|-------------|
| audience | Complete beginners with zero technical knowledge |
| structure | Numbered steps, one action per step |
| platform | macOS primary, Windows noted where different |

## Relationships

```
README.md (entry point)
  └── references → field-guide.html (via GitHub Pages URL)
  └── references → /starter command (final setup step)

/starter command
  └── depends on → commands/ (verifies they exist)
  └── depends on → skills/ (counts them in summary)
  └── depends on → git repo (runs git pull)

index.html
  └── redirects → field-guide.html
```

## State Transitions

None. All files are static and immutable from the user's perspective.
Updates arrive via `git pull` which replaces file contents atomically.
