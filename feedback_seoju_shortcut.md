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

**How to apply:** On receiving `seoju`, cd into `/mnt/c/project/dev/erp`, default exploration to `2_WORKS/work-vsc-2th` (Vue), `2_WORKS/work-eclipse-2th` (Java), `files`, and `lib` per [[project_scope_and_stack]] (same internal structure as the company path, just under a different root), and frame subsequent explanations assuming ERP-domain familiarity per [[user_role]]. Confirm the switch briefly, then wait for the user's actual task. If `/mnt/c/project/dev/erp` doesn't exist in the current environment, this is the company PC, not home — the folder's absence is itself sufficient signal, no separate check is needed; suggest `dcos` instead.
