---
name: project-wsl-environment-ephemeral
description: "This WSL/Linux environment (incl. local PostgreSQL used by the seoju stock project) only runs while a Claude Code session is connected — it boots fresh each session and goes down on disconnect, so nothing in it is an always-on service"
metadata: 
  node_type: memory
  type: project
  originSessionId: 4b2319be-253b-4561-856b-5058082548d1
---

Confirmed 2026-07-02: system `uptime` and the `postgresql` systemd service's start timestamp matched exactly (both ~13 min, since session start) — i.e. this Linux environment boots when a Claude Code session connects, not independently. Opening a direct PostgreSQL connection (e.g. from a Windows GUI client) while no Claude Code session is active fails/disconnects, because the whole environment the DB lives in isn't running at that point.

**Why:** Relevant to [[project_stock_feature_progress]] — the local `seoju` Postgres DB (stock schema: item/watchlist/price_daily) and any future Java batch collector live in this same ephemeral environment.

**How to apply:** Don't design the stock data-collection batch (KIS API puller) as something expected to run on its own schedule (cron/systemd timer) independent of Claude Code sessions — it won't fire while disconnected. If the user wants truly always-on daily collection, it needs to run somewhere persistent (native Windows/WSL2 distro outside Claude's environment, a real server, or a cloud scheduler), not inside this session-bound environment. Worth surfacing this constraint explicitly if/when batch scheduling design resumes.
