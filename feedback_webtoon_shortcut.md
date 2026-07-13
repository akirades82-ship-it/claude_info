---
name: feedback-webtoon-shortcut
description: "'webtoon' typed as a message is a shortcut to switch to the HOME PC's webtoon project folder (/mnt/c/project/webtoon), a new personal creative project separate from ERP/stock work"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 632dce49-73fd-4ea5-b181-d5bd14afe188
---

When the user types just `webtoon` as a message, treat it as a shortcut meaning: on the **home PC**, switch working context to `C:\project\webtoon` (WSL path `/mnt/c/project/webtoon`).

**Why:** Same shortcut-word pattern as [[feedback_seoju_shortcut]] (home ERP/stock context) and [[feedback_dcos_shortcut]] (company ERP context) — a dedicated keyword avoids ambiguity about which of the user's several home-PC projects is active. Unlike `seoju`, this is a brand-new, separate personal project — do not apply the ERP-developer framing from [[user_role]]/[[project_scope_and_stack]] here, and do not carry over stock-project state ([[project_stock_screening_goal]]) into a `webtoon` session or vice versa. Keep this project's context distinct from `seoju`'s, per [[feedback_personal_vs_work_separation]]'s general principle of not bleeding context between the user's separate home-PC threads.

**Memory lives in a SEPARATE repo (2026-07-13, user's explicit request):** unlike every other project on this list, webtoon memory is NOT in this `claude_info` repo — it's split into its own private repo `claude_info_dcos`-style: **`https://github.com/akirades82-ship-it/claude_info_webtoon`**, checked out locally at **`/root/.claude/webtoon-memory/`** (separate git working tree, own `MEMORY.md`/`README.md`, not on Claude's auto-loaded memory path). Contains [[project_webtoon_goal]] (the confirmed "가족 프로필" cast/style and Gemini-prompt workflow) and will hold all future webtoon-project memory.

**How to apply:** On receiving `webtoon`, cd into `/mnt/c/project/webtoon` for the actual project files, AND separately read `/root/.claude/webtoon-memory/MEMORY.md` (run `git -C /root/.claude/webtoon-memory pull` first in case it changed elsewhere) for the project memory — it won't be in this repo or auto-loaded. After creating/editing memory content for webtoon, commit+push inside `/root/.claude/webtoon-memory` (its own `git add -A && git commit && git push`), separate from this repo's own commit/push. Don't assume it's ERP-related or reuse seoju/stock framing — this is a distinct personal creative project.
