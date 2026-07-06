---
name: feedback-trust-explicit-user-schema-over-inference
description: "When a user explicitly states a DB table's full column list, trust it literally over inferences drawn from partial error messages (e.g. SQL error ordering)"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: b6ec325d-13a4-43af-b28c-cbe16563113d
---

If a user states a table's schema explicitly (e.g. pastes a full column list, especially more than once), treat that as ground truth — don't override it with a clever-sounding inference from indirect evidence like which column an ORA-00904 happened to name first.

**Why:** On [[project_mangi_gift_mng_popup]], the user pasted `TB_MEMBER_MANGI_GIFT_MNG`'s column list (SEQ, INSERT_GBN, M_PERIOD_CD, GIFT_CODE, DEL_FG — 5 columns, no audit columns) twice. After a `ORA-00904: UPD_DM invalid identifier` error, the reasoning "the error only named UPD_DM, so REG_MAN/REG_DM/UPD_MAN earlier in the SELECT list must be valid" was applied and only `UPD_DM` was stripped from the queries. This was wrong — the user then had to explicitly repeat the schema a third time to correct it. Oracle's column-resolution error ordering doesn't reliably match SELECT-list textual order (especially inside nested/paginated subqueries), so it's weak evidence at best and shouldn't outrank an explicit, repeated user statement.

**How to apply:** When a schema mismatch bug is reported and the user has already told you the columns, fix the code to match that literal list first — don't partially fix based on which specific error surfaced, since more of the same class of error are usually still hiding behind the first one. Only fall back to inferring schema from error messages when the user hasn't stated it. If DB introspection tools aren't available (as in this WSL session — no sqlplus/oracledb client), say so explicitly rather than presenting an inference as if verified.
