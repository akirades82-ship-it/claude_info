---
name: project-home-erp-goal
description: "The home ('seoju') project is NOT a 1:1 clone of the company ERP — it's the user's own ERP system, using the company codebase as a reference/inspiration only. Direction/scope still undecided."
metadata: 
  node_type: memory
  type: project
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

At home ([[feedback_seoju_shortcut]], `/mnt/c/project/dev/erp`), the user is not trying to replicate every form/module of the company ERP ([[feedback_dcos_shortcut]], `/mnt/c/IW-DEV`). They're building their **own** ERP system, using the company project's structure, code, and DB schema (e.g. `LF_DMUSER.MEMBER` etc.) only as a reference to learn from and port ideas out of — not as a spec to fully mirror.

As of 2026-07-01, the user hasn't decided the concrete purpose/direction yet (e.g. whether it'll be a real business-use ERP, a learning project, or something narrower) — they said they'll figure it out as they go, starting from whatever feature they touch first.

**Why:** Came up right after building a PostgreSQL `member` table that mirrored the Oracle `LF_DMUSER.MEMBER` columns closely — the user clarified the home project doesn't need full parity with the company system.

**How to apply:** Don't assume every company-side table/module/form needs to be reproduced at home. When porting something from the company codebase for the home project, treat the original as a reference to adapt/simplify rather than a contract to match exactly — check with the user on scope/fidelity when it's ambiguous, rather than defaulting to full replication. Since direction is still open, stay flexible rather than optimizing for one assumed end-goal.
