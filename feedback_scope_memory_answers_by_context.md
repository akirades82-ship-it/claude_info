---
name: feedback-scope-memory-answers-by-context
description: "When answering 'what's the last memory' or similar recall questions, filter to the current context (dcos company vs seoju home) first — don't just pick the most-recently-modified file"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 137d2d63-6912-466c-947b-fdaa77035766
---

Mistake made 2026-07-06: user typed `seoju` to switch to home context, then asked "마지막 메모리" (last memory). I answered with `project_mangi_gift_mng_popup.md` (TB_MEMBER_MANGI_GIFT_MNG, DlwMangiMngController) purely because it had the latest mtime — but that memory is real company (`dcos`/`/mnt/c/IW-DEV`) production work, not seoju. User corrected: "이건 회사꺼 잖아 난 seoju 인데".

**Why this is confusing:** [[feedback_personal_vs_work_separation]] notes the seoju home project structurally clones the company repo (`work-vsc-2th`/`work-eclipse-2th` exist under both `/mnt/c/IW-DEV` and `/mnt/c/project/dev/erp`), so file-path/folder-name pattern alone can't distinguish which context a piece of work happened in. Real production business tables/controllers (e.g. `TB_MEMBER_*`, `Dlw*Controller`) are a strong signal of company (`dcos`) work; seoju's own domain is personal docs + stock data ([[project_home_erp_goal]], [[project_stock_screening_goal]], [[project_stock_feature_progress]]).

**How to apply:** Before answering any "last memory" / recall-style question, first check which context (`dcos` vs `seoju`) is currently active, then filter candidate memories to that context by content domain (business/production ERP tables = dcos; personal docs/stock/myerp = seoju) — not just by file mtime. If ambiguous, ask rather than assume the newest file is relevant.
