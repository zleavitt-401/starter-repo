---
name: rules-generator
description: Use when creating, designing, or organizing .claude/rules/ files for any project. Triggers when user wants to set up rules for a new or existing project, migrate content from CLAUDE.md into modular rules, create path-scoped rules for specific file types or folders, or asks about what rules a project needs.
---

# Claude Rules Generator

## Overview

Generates well-structured `.claude/rules/` files for projects. Rules are modular instruction files that Claude Code loads automatically — globally or only when working on specific file paths.

**Key distinction from CLAUDE.md:**
- `CLAUDE.md` = always loaded, global, kept short (under ~150 lines)
- `.claude/rules/*.md` = modular, can be path-scoped, loaded on demand

---

## When to Use Rules vs CLAUDE.md

| Put in CLAUDE.md | Put in .claude/rules/ |
|---|---|
| Project overview, stack, deployment | Detailed coding standards |
| Core commands (dev, build, test) | Framework-specific patterns |
| Universal rules (applies every session) | Path-specific file conventions |
| Links/pointers to rules files | Security checklists |

**Rule of thumb:** If CLAUDE.md is approaching 100+ lines, move topic-specific sections to rules files.

---

## Step 1: Interview the Project

Before creating any files, gather this information:

1. **What's the stack?** (languages, frameworks, libraries)
2. **What file structure exists?** (src/, api/, components/, etc.)
3. **What problems have come up?** (repeated mistakes Claude makes, inconsistencies)
4. **Are there existing CLAUDE.md rules to migrate?**
5. **Any specific domains that need focused rules?** (security, testing, Firebase, TypeScript, etc.)

---

## Step 2: Design the Rules Architecture

### Common rule files by project type

**Vanilla JS / Zero-build projects (like Zach's stack):**
```
.claude/rules/
├── javascript.md         # ES6+, module patterns, async/await
├── firebase.md           # Firebase-specific patterns (path-scoped to firebase files)
├── security.md           # API keys, auth, input sanitization
└── deployment.md         # Vercel-specific, env vars, build steps
```

**TypeScript projects:**
```
.claude/rules/
├── typescript.md         # Types, interfaces, strict mode — scoped to *.ts files
├── testing.md            # Test patterns — scoped to *.test.ts files
└── api.md                # API conventions — scoped to api/**
```

**Multi-feature projects:**
```
.claude/rules/
├── general.md            # Universal rules (no paths frontmatter)
├── frontend/
│   ├── components.md     # Scoped to src/components/**
│   └── styles.md         # Scoped to *.css, *.scss
└── backend/
    ├── api.md            # Scoped to api/**
    └── database.md       # Scoped to db/** or firebase/**
```

---

## Step 3: Write Each Rule File

### File anatomy

```markdown
---
paths:
  - "src/api/**/*.ts"
---

# API Development Rules

Brief description of what this covers.

## Conventions
- Specific, actionable rules only
- No rules Claude already follows by default
- Prefer "always do X" over "try to do X"

## Patterns
[Code examples if helpful — keep short]

## Never Do
- Anti-patterns specific to this project
```

### Frontmatter rules (critical)

**Global rule (loads every session):**
```markdown
# no frontmatter needed — just start with #
# Content here
```

**Path-scoped rule (only loads for matching files):**
```markdown
---
paths:
  - "src/**/*.ts"
  - "lib/**/*.ts"
---
```

**⚠️ Important gotchas:**
- Always quote glob patterns in YAML (`"**/*.ts"` not `**/*.ts`)
- Don't use `alwaysApply: true` — that's Cursor syntax, not Claude Code
- Path patterns are relative to repo root
- Use standard glob: `*` matches anything except `/`, `**` matches across directories
- As of early 2026, path-scoping has known bugs in some Claude Code versions — test it

### Content quality rules

**Be specific, not vague:**
```markdown
# ❌ Bad
- Write clean code

# ✅ Good  
- Use async/await, never .then() chains
- Destructure function parameters when there are 3+ args
```

**Don't repeat Claude's defaults:**
```markdown
# ❌ Wasteful — Claude already does this
- Use meaningful variable names
- Handle errors properly

# ✅ Project-specific value
- All Firebase errors must log to console with the operation name
- Never expose Firebase config in client-side code beyond the init object
```

**Keep each rule file under ~50 lines.** If longer, split into sub-files.

---

## Step 4: Output the Files

For each rule file, output:
1. The full file path (e.g., `.claude/rules/firebase.md`)
2. The complete file content
3. A one-line note on when it loads

Then provide a summary showing the full directory tree.

---

## Zach's Stack Reference

For Zach's projects (Fauxbituaries, Conglomerate, Bionic Reader):

**Common rules worth creating:**
- `firebase.md` — scoped to files touching Firebase (init, auth, firestore calls)
- `security.md` — global, covers API key handling, input sanitization, XSS
- `typescript.md` — scoped to `**/*.ts` files (relevant for Bionic Reader)
- `javascript.md` — global JS conventions for vanilla JS projects
- `vercel.md` — deployment rules, env var naming, serverless function patterns

**CLAUDE.md should keep:**
- Project name + 2-sentence purpose
- Stack overview (tech, versions)
- Key commands (dev, deploy)
- Pointers to rules files

---

## Common Mistakes to Avoid

| Mistake | Fix |
|---|---|
| Unquoted globs in YAML | Always quote: `"**/*.ts"` |
| Using `alwaysApply` | Omit frontmatter for global rules |
| Rules longer than 80 lines | Split into focused sub-files |
| Duplicating what's in CLAUDE.md | Keep CLAUDE.md as index, rules as detail |
| Over-scoping paths | Test that paths match your actual file structure |
| Rules that are too vague | Every rule should be checkable / actionable |
