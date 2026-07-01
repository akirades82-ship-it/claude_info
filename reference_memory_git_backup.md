---
name: reference-memory-git-backup
description: "Claude memory is now git-backed at /root/claude-memory, synced to a GitHub repo"
metadata:
  type: reference
---

`/root/.claude/memory` is a symlink to `/root/claude-memory`, which is a git repo with remote `https://github.com/akirades82-ship-it/claude_info.git` (branch `main`). GitHub auth is via `gh` CLI (logged in as `akirades82-ship-it`).

**How to apply:** After creating or editing memory files, `cd /root/claude-memory && git add -A && git commit -m "..." && git push` to keep the GitHub backup current. If this repo is ever missing on a new machine, `git clone` it to `/root/claude-memory` and symlink `/root/.claude/memory` to it to restore all memory.
