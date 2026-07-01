---
name: feedback-seoju-auto-journal
description: "Proactively write a dated .txt note whenever a meaningful decision/direction change happens on the seoju home project, without waiting for the user to say '기록하자' each time"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

For the [[feedback_seoju_shortcut]] / [[project_home_erp_goal]] work (personal ERP-style system: docs + stock data), proactively create a timestamped text note whenever something meaningful happens — a strategy/direction decision, a scope change, a completed milestone, a design choice with reasoning — instead of only doing it when the user explicitly asks to record it (as they did once for the swing-trading strategy discussion).

**Why:** The user wants to be able to look back in ~3 months and check whether the project is still headed the right way, using these notes as a trail of what was decided and why. They explicitly said they shouldn't have to ask each time — it should happen automatically at the "meaningful decision/direction change" level, not for every message and not only at session end.

**How to apply:** Save notes as `YYYYMMDD_HHMMSS_<short-topic>.txt` under `/mnt/c/project/stock` (or the analogous folder for whatever sub-area of the seoju project is active — ask if a new sub-area doesn't have an obvious folder yet), get the real timestamp via a `date` shell command rather than guessing it. Keep each note short and focused: what was decided/concluded, the key reasoning/tradeoffs, and open next steps — mirror the style of the first note (`20260701_225618_swing_strategy_note.txt`). Don't journal routine/mechanical steps (e.g. running a command, creating a table) unless they represent a decision point; do journal things like "chose KIS API over X", "decided swing screening should use multi-timeframe bars, not news", "postponed implementation to gather study material first". Per [[feedback_personal_vs_work_separation]], this only applies in the seoju/home context, never during company (dcos) sessions.
