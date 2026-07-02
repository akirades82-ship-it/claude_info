---
name: feedback-seoju-shortcut
description: "'seoju' typed as a message is a shortcut to switch to the HOME PC's ERP project folder (/mnt/c/project/dev/erp), the home equivalent of [[feedback_dcos_shortcut]]"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

When the user types just `seoju` as a message, treat it as a shortcut meaning: on the **home PC**, switch working context to `/mnt/c/project/dev/erp` and apply the ERP-developer framing from [[user_role]] and [[project_scope_and_stack]]. This is the home-PC counterpart to `dcos` (company PC, `/mnt/c/IW-DEV`) — same project, different root folder per machine.

**Why:** The user works on this ERP project from both a company PC and a home PC, and each machine has its own root folder for the same codebase. A separate shortcut word per machine avoids ambiguity about which root to use.

**How to apply:** On receiving `seoju`, cd into `/mnt/c/project/dev/erp`, default exploration to `2_WORKS/work-vsc-2th` (Vue), `2_WORKS/work-eclipse-2th` (Java), `files`, and `lib` per [[project_scope_and_stack]] (same internal structure as the company path, just under a different root), and frame subsequent explanations assuming ERP-domain familiarity per [[user_role]]. If `/mnt/c/project/dev/erp` doesn't exist in the current environment, this is the company PC, not home — the folder's absence is itself sufficient signal, no separate check is needed; suggest `dcos` instead.

**Continuing across sessions:** Each `seoju` session is a fresh conversation with no memory of prior chats except what's saved here — the user explicitly wants it to feel like picking the conversation back up, not starting over. So before just "confirming the switch and waiting," proactively check [[project_stock_screening_goal]] (and [[project_stock_feature_progress]] if that thread is cold) for the current state of the active seoju/myerp work, and open with a short recap of where things stand (what was last built/decided, what's the open next step) rather than a bare "전환했습니다, 뭐 도와드릴까요?". Also worth a quick `systemctl status postgresql myerp-backend myerp-frontend` and a check of whether `stock.price_daily`'s latest date is current, since the environment/data may or may not have been kept fresh since the last session (see [[project_wsl_environment_ephemeral]]) — mention it if stale rather than assuming.
