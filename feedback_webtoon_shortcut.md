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

**Project state as of 2026-07-13 (very early):** folder contains only 3 Gemini-generated images (`Gemini_Generated_Image_*.png`), no code/project structure yet. Looks like an AI-image-assisted webtoon/comic creation project just getting started — actual goal/scope not yet stated by the user, don't assume beyond what's there. Update this memory once the project's actual purpose and tooling are clarified.

**How to apply:** On receiving `webtoon`, cd into `/mnt/c/project/webtoon` and ask what the user wants to do if the goal isn't already clear from context — don't assume it's ERP-related or reuse seoju/stock framing.
