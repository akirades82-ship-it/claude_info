---
name: reference-memory-git-backup
description: "Claude memory is now git-backed at /root/claude-memory, synced to a GitHub repo"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

The Claude Code memory directory itself is a git repo with remote `https://github.com/akirades82-ship-it/claude_info.git` (branch `main`). GitHub auth is via `gh` CLI (logged in as `akirades82-ship-it`). Note: the exact memory directory path varies by environment/harness version — it has been seen as both `/root/.claude/memory` and `/root/.claude/projects/-/memory`; always resolve the current path rather than assuming one.

**How to apply:** After creating or editing memory files, `cd <current memory dir> && git add -A && git commit -m "..." && git push` to keep the GitHub backup current. To restore/sync on a new machine/container: install `gh` if missing, run `gh auth login` (browser device-code flow works even without a prior PAT, as long as the user is logged into GitHub in a browser), then in the memory directory run `git init`, `git remote add origin https://github.com/akirades82-ship-it/claude_info.git`, `git fetch origin main`, `git checkout -B main origin/main`. Caution: if memory is edited on two machines at once without pulling in between, git merge conflicts can occur — pull before editing when in doubt.

**Automated sync (as of 2026-07-02):** A `SessionStart` hook in `/root/.claude/settings.json` runs this pull/bootstrap automatically at the start of every session (`mkdir -p` the memory dir, then `git pull origin main` if already a repo, else `git init` + remote add + fetch + checkout `main`) — shows as "Syncing memory from GitHub..." at session start. So memory is already current from GitHub by the time a conversation begins; no manual pull needed before reading memory. Manual push after edits is still required (the hook only pulls, it doesn't push).
