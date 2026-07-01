---
name: project-home-erp-goal
description: "The home ('seoju') project is NOT a 1:1 clone of the company ERP. It's a personal system for organizing documents and aggregating stock-market data, built by reusing some ERP-style features (real-time inquiry, data management screens) from the company codebase as reference."
metadata: 
  node_type: memory
  type: project
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

At home ([[feedback_seoju_shortcut]], `/mnt/c/project/dev/erp`), the user is not trying to replicate every form/module of the company ERP ([[feedback_dcos_shortcut]], `/mnt/c/IW-DEV`). They're building their **own** system, using the company project's structure, code, and DB schema (e.g. `LF_DMUSER.MEMBER` etc.) only as a reference to learn from and port ideas out of — not as a spec to fully mirror.

**Concrete goal (as of 2026-07-01):** the `seoju` project combines (1) general dev work/practice, (2) organizing various personal documents, and (3) collecting/aggregating stock-market-related data into a usable dataset — then reusing a *subset* of ERP-style features (real-time inquiry/lookup screens, data management CRUD) from the company codebase to browse and manage that document + stock data. So the "ERP" part is really a UI/architecture pattern being repurposed for personal document + stock data management, not a business-domain clone (member/billing/product/etc. don't need to carry over as concepts).

**Why:** Initially the user said direction was undecided; they then clarified concretely that the project's real purpose is personal document organization + stock data aggregation with ERP-style real-time inquiry/management screens on top — not a member/customer/billing-style ERP business domain.

**How to apply:** Don't assume every company-side table/module/form needs to be reproduced at home, and don't default to recreating company business-domain tables (like `MEMBER`, `billing`, `partner`) unless the user is explicitly modeling personal-domain data (documents, stock holdings/prices/watchlists, etc.) through them. When porting something from the company codebase, treat it as a reference for *how to build a real-time inquiry/data-management screen*, and ask what personal-domain entity it should actually apply to. Also see [[feedback_personal_vs_work_separation]] — this stock/document content must not surface in company (`dcos`) sessions.
