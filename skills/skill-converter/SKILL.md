---
name: skill-converter
description: Use when porting a skill from Claude.ai to Claude Code, or from Claude Code to Claude.ai. Triggers when user wants to use a skill in the other platform, asks to convert a skill, or says a skill "works in one place but not the other." Also use when a user has a .skill file they want to install in Claude Code, or a ~/.claude/skills/ folder they want to upload to Claude.ai.
---

# Skill Converter

Converts skills between Claude.ai format (`.skill` files) and Claude Code format (`~/.claude/skills/` folders) in either direction.

## Quick Decision

```
User has a skill and wants it in the other platform?
  → Ask which direction (if not obvious)
  → Assess compatibility (see below)
  → Convert and deliver
```

## Format Differences

| | Claude.ai | Claude Code |
|---|---|---|
| **File format** | Single `.skill` file (zipped folder) | Folder with `SKILL.md` + optional files |
| **Trigger** | Name + description in system prompt | Name + description in system prompt |
| **SKILL.md** | Same structure | Same structure |
| **Package install** | Can install npm/PyPI at runtime | ❌ No runtime installs |
| **Subagents** | ❌ Not available | ✅ Available |
| **Artifacts UI** | ✅ (panel, download button) | ❌ |
| **bash access** | ✅ Limited (code execution tool) | ✅ Full shell |
| **File output** | `/mnt/user-data/outputs/` | User's project directory |

## Compatibility Assessment

Before converting, flag these issues:

**🔴 Breaks entirely — needs rewrite:**
- Skill relies on subagents → Claude.ai has none; simplify to sequential steps
- Skill references Claude Code-only tools (`TodoWrite`, `Task`, worktrees)

**🟡 Needs adaptation — minor edits:**
- Package installs (`pip install X`, `npm install X`) → Pre-assume installed; add note to user
- File output paths (`/mnt/user-data/outputs/`) → Change to relative paths or project dir
- References to "artifacts panel" or "download button" → Rephrase for context

**🟢 Ports cleanly — just reformat:**
- Pure instructional content (how to use a library, patterns, best practices)
- Reference material (API docs, code examples)
- Workflow steps that don't use platform-specific tools

The d3-viz skill is a perfect 🟢 example — it's all instructional JS content.

## Direction: Claude Code → Claude.ai

**Input:** A `SKILL.md` file (and any supporting files) from `~/.claude/skills/skill-name/`

**Steps:**
1. Read the `SKILL.md` and all files in the skill folder
2. Run compatibility assessment above
3. Adapt any flagged content
4. Package as a `.skill` file using the bash script below
5. Deliver via `present_files`

```bash
# Package a skill folder into a .skill file
cd /home/claude
cp -r /path/to/skill-name ./skill-name-temp
cd skill-name-temp
zip -r ../skill-name.skill .
cd ..
rm -rf skill-name-temp
```

**Tell the user:** "Upload this `.skill` file to your Claude.ai project via Settings → Skills."

## Direction: Claude.ai → Claude Code

**Input:** A `.skill` file the user has uploaded, OR the user pastes the skill content directly

**Steps:**
1. If `.skill` file: unzip it to inspect contents
2. Run compatibility assessment above
3. Adapt any flagged content
4. Create the folder structure at `/mnt/user-data/outputs/skill-name/`
5. Write `SKILL.md` and any supporting files
6. Deliver via `present_files`

```bash
# Unzip a .skill file to inspect
mkdir -p /home/claude/skill-inspect
cp /mnt/user-data/uploads/skill-name.skill /home/claude/skill-inspect/
cd /home/claude/skill-inspect
unzip skill-name.skill
```

**Tell the user:** "Copy the `skill-name/` folder to `~/.claude/skills/` on your machine."

## Content Adaptation Rules

### Subagents (Claude Code only)
If a skill uses subagents, replace with sequential instructions for Claude.ai:
```
# Before (Claude Code)
Spawn a subagent to run each test case in parallel.

# After (Claude.ai)
Run each test case sequentially. For each test case:
1. Read the SKILL.md
2. Follow its instructions to complete the task
3. Record the output
```

### Package dependencies
```
# Before
Run: pip install pandas --break-system-packages

# After (Claude.ai)
Assumes pandas is available. If not, install it first via the code execution tool.
```

### File output paths
```
# Before (Claude.ai)
Save output to /mnt/user-data/outputs/

# After (Claude Code)
Save output to the user's project directory (ask if unclear).
```

### Artifacts UI references
```
# Before (Claude.ai)
The user can download the file via the artifact panel.

# After (Claude Code)
The file will be saved to the project directory.
```

## SKILL.md Frontmatter Rules (both platforms)

Keep these exactly the same when converting — they're identical across platforms:
- `name`: letters, numbers, hyphens only — no reserved words (don't use `claude`)
- `description`: max ~500 chars, third-person, starts with "Use when..."
- No other frontmatter fields are supported

## Example: Porting d3-viz

The d3-viz skill is pure instructional content — it's a 🟢 clean port. No adaptation needed. Just:
- Claude Code → Claude.ai: zip the folder into `d3-viz.skill`
- Claude.ai → Claude Code: unzip to `~/.claude/skills/d3-viz/`

The SKILL.md content stays identical.

## Delivery Checklist

- [ ] Compatibility issues flagged and resolved
- [ ] SKILL.md frontmatter valid for target platform
- [ ] Adapted content noted with comments so user knows what changed
- [ ] File packaged in correct format for target platform
- [ ] Clear install instructions given to user
