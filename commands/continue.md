---
description: Generate a prompt to continue the current work in a new chat.
---

Review the full conversation to understand what we've been working on, then generate a **continuation prompt** that I can paste into a new chat to pick up where we left off.

The prompt should include:

1. **Context** — What project/feature we're working on and the current branch
2. **What was accomplished** — Key changes made in this session (files modified, features implemented, commits made)
3. **Current state** — Where things stand right now (what's deployed, what's pending, any open issues)
4. **Next steps** — What remains to be done or what we were about to do when the session ended
5. **Key decisions** — Any important decisions or constraints established during the session that the next chat needs to know

Format the output as a single fenced code block that I can copy directly. Keep it concise but complete enough that the new chat can continue without re-discovering context.
