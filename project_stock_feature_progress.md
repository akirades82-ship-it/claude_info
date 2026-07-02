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

**Also done (2026-07-02):** copied the company's design CSS (`comm.css`/`admin.css`/`homebox.css`/`portal.css`/`system.css`/`rdcs.css`) and Noto Sans KR font files from `work-vsc-2th/powerservice-vue` into `myerp/frontend/src/assets/theme`, wired into `main.js`. Font is freely reusable (Google, SIL OFL license). The CSS itself is the company's own proprietary code (not a purchased license like Kendo, but still a confidentiality/IP consideration) — user was informed and explicitly chose to copy it as-is anyway; this was their call to make.

Confirmed via web search that KIS Developers API covers everything needed for the swing-screening priority list: daily/weekly/monthly/yearly candles (국내주식기간별시세), index history (국내업종 일자별지수 / 국내주식업종기간별시세), and investor flow data (종목별 투자자매매동향(일별), 시장별 투자자매매동향(일별), 종목별 외국계 순매수추이, 종목별 외인기관 추정가집계). Minute candles exist too (주식당일분봉조회 = today only, 주식일별분봉조회 = specific past date, one day per call) — so intraday history is retrievable, just not in one bulk range call.

**Paused again (2026-07-02):** user is switching to company (`dcos`) work starting tomorrow; this stock/seoju thread is on hold until they come back to it.

**Scope guardrail (2026-07-02, confirmed explicitly by user):** This project is data collection + swing-candidate screening ONLY. The user does NOT want automated buy/sell order execution, ever. KIS API integration must stick to quotation/read-only endpoints (시세/차트/수급) — never implement or wire up KIS's order-placement (매수/매도 주문) endpoints, even though the KIS account used is a 실전투자 (live) account (chosen only because some quote data may be unsupported on 모의투자, not because live trading was wanted). App Key/Secret stored in `/etc/myerp/kis.env` (mode 600, user fills in directly, never pasted in chat) — same pattern as [[project_wsl_environment_ephemeral]]'s `backend.env`.

**Infra change (2026-07-02, later same day):** myerp made independent of Claude Code sessions — see [[project_wsl_environment_ephemeral]] for the full why/how. Concretely: `myerp-backend.service` runs `java -jar backend/target/myerp-backend-0.1.0.jar` (port 8080), DB password comes from `/etc/myerp/backend.env` (`SEOJU_DB_PASSWORD=`, currently still the placeholder `CHANGE_ME` — must be filled in before the backend will actually start). `myerp-frontend.service` serves the built `frontend/dist/` statically via `python3 -m http.server 8081` (chosen over the `yarn serve` dev server for a lighter always-on footprint) — means frontend code changes need `yarn build` + `systemctl restart myerp-frontend` to show up, not live-reloaded. Both are `systemctl enable`d so they start automatically once the WSL box is up.

**How to apply:** When resuming this thread, check `/mnt/c/project/stock` for material/notes the user has since added — it may clarify direction/requirements before writing more code. Don't restart the KIS API/Java-batch design from scratch; the open questions are specifically API credential status and module placement (new module in `work-eclipse-2th` vs. standalone Java project), not the overall approach. Do NOT reintroduce Kendo/other paid UI libraries without the user explicitly opting in with their own valid license — default to free/open-source (Element Plus, Chart.js, etc.). Data collection priority already decided: daily OHLCV+volume (broad universe, not just the watchlist) → index daily data → investor flow (수급) → minute candles last, for entry timing only.
