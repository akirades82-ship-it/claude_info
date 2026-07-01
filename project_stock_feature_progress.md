---
name: project-stock-feature-progress
description: "Progress and next steps on the seoju home project's stock watchlist/price feature — DB schema built, KIS Developers API + Java batch chosen as direction, now paused for user to gather study material in /mnt/c/project/stock"
metadata: 
  node_type: memory
  type: project
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

Part of the [[project_home_erp_goal]] effort. Status as of 2026-07-01:

**Done:**
- Local PostgreSQL 18 installed and running in this WSL environment (port 5432). Databases: `gocs` (mirrors the company project's leftover `gocs` datasource, empty/unused) and `seoju` (the user's own DB, superuser role `seoju`).
- In `seoju` DB: created schema `stock` with tables `stock.item` (종목 마스터: item_cd PK, item_nm, market_cl), `stock.watchlist` (관심종목: item_cd FK, memo), `stock.price_daily` (일별 시세: item_cd+trade_dt composite PK, open/high/low/close/volume). Scope decided: 국내 주식(코스피/코스닥), 일별 종가 배치 수집 (not real-time/intraday).
- Also earlier created a `member` table in `seoju` modeled on the company's `LF_DMUSER.MEMBER` (from `powerservice` mapper XML) — this was built before the user clarified the project's real domain is personal docs + stock data, so it may not actually be needed; left in place, not yet removed.
- Direction chosen for data collection: 한국투자증권 KIS Developers API, Java batch (not Python/cron script). NOT yet decided: whether the user already has KIS Developer App Key/Secret issued, and whether the batch should live inside the existing `work-eclipse-2th` Eclipse/Maven workspace as a new module or as a fully separate Java project.

**Paused — user's stated next step:** before continuing implementation, the user wants to gather stock-related reference material/documents and study first. Created `/mnt/c/project/stock` (sibling to `dev/erp`, outside the ERP git repo) as the place to drop that material. Detailed dated notes on decisions/progress live as `.txt` files in that folder per [[feedback_seoju_auto_journal]] — check there for the latest state, this memory just gives the standing overview.

**Also done (2026-07-01, after the pause was first noted):** started a first concrete app skeleton at `/mnt/c/project/dev/myerp` (`backend/`, `frontend/`) — separate from the reference `dev/erp` clone. Goal: a lightweight "현황판" (status board) screen, not a full app, showing the watchlist + recent prices + a simple chart.
- Backend: Spring Boot 3.3 (Java 21) + MyBatis + PostgreSQL (`seoju` db), exposing `GET /api/dashboard/watchlist` and `GET /api/dashboard/prices/{itemCd}`. DB password passed via `SEOJU_DB_PASSWORD` env var, not hardcoded.
- Frontend: Vue 3 + vue-cli-service (matches company `work-vsc-2th` tooling), port 8081. Grid/chart were originally built with Kendo Vue, but swapped to **Element Plus (`el-table`) + Chart.js (`vue-chartjs`)** after concluding the company's Kendo license (org-owned seat license) can't legitimately be reused for this personal project, and the user didn't want to activate their own personal Kendo license for this yet — free/open-source only, moving forward, unless the user explicitly says otherwise.
- Runtimes installed in this WSL environment to support this: Java 21 (openjdk-21-jdk-headless), Maven, Yarn (via corepack).

**How to apply:** When resuming this thread, check `/mnt/c/project/stock` for material/notes the user has since added — it may clarify direction/requirements before writing more code. Don't restart the KIS API/Java-batch design from scratch; the open questions are specifically API credential status and module placement (new module in `work-eclipse-2th` vs. standalone Java project), not the overall approach. Do NOT reintroduce Kendo/other paid UI libraries without the user explicitly opting in with their own valid license — default to free/open-source (Element Plus, Chart.js, etc.).
