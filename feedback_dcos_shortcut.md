---
name: feedback-dcos-shortcut
description: "'dcos' typed as a message is a shortcut to switch to the COMPANY IW-DEV project folder with ERP context applied (see [[feedback_seoju_shortcut]] for the home-PC equivalent)"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 67f83087-9a8b-49d3-81eb-019d2726523e
---

When the user types just `dcos` as a message, treat it as a shortcut meaning: on the **company PC**, switch working context to `/mnt/c/IW-DEV` and apply the ERP-developer framing from [[user_role]] and [[project_scope_and_stack]]. The home-PC equivalent shortcut is `seoju`, which points to `/mnt/c/project/dev/erp` instead — see [[feedback_seoju_shortcut]].

**Why:** User wants a quick way to re-enter their ERP project context without retyping the folder path or role description each time. Company and home PCs use different root folders for the same project, so a machine-specific shortcut word was introduced for each.

**How to apply:** On receiving `dcos`, cd into `/mnt/c/IW-DEV`, default exploration to `2_WORKS/work-vsc-2th` (Vue), `2_WORKS/work-eclipse-2th` (Java), `files`, and `lib` per [[project_scope_and_stack]], and frame subsequent explanations assuming ERP-domain familiarity per [[user_role]]. Confirm the switch briefly, then wait for the user's actual task. If `/mnt/c/IW-DEV` doesn't exist in the current environment, this is likely the home PC — suggest `seoju` instead.
