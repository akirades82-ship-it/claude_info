---
name: reference-memory-git-backup
description: "Claude memory is now git-backed at /root/claude-memory, synced to a GitHub repo"
metadata:
  type: reference
---

`/root/.claude/memory` is a symlink to `/root/claude-memory`, which is a git repo with remote `https://github.com/akirades82-ship-it/claude_info.git` (branch `main`). GitHub auth is via `gh` CLI (logged in as `akirades82-ship-it`).

**How to apply:** After creating or editing memory files, `cd /root/claude-memory && git add -A && git commit -m "..." && git push` to keep the GitHub backup current. To restore/sync on another machine: `gh auth login`, then `git clone https://github.com/akirades82-ship-it/claude_info.git ~/claude-memory`, then symlink that machine's `~/.claude/memory` to it. Caution: if memory is edited on two machines at once without pulling in between, git merge conflicts can occur — treat one machine as primary or pull before editing.
