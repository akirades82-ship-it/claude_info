---
name: project-stock-screening-goal
description: "The seoju stock project's concrete target and methodology: find candidates likely to return +10% within 15 trading days, using technical patterns validated by backtest (not assumed), user is a trading beginner relying on Claude to design/validate the method"
metadata: 
  node_type: memory
  type: project
  originSessionId: 4b2319be-253b-4561-856b-5058082548d1
---

Confirmed 2026-07-02. Part of [[project_stock_feature_progress]] / [[project_home_erp_goal]].

**User's expertise level:** Stock trading beginner — only knows how to place buy/sell orders. Can understand and act on data/analysis when it's explained conversationally, but is relying on Claude to actually design and validate the screening methodology, not just build infrastructure. This is different from earlier assumptions — the user isn't bringing their own trading strategy for Claude to implement; Claude needs to propose candidate technical patterns and prove them out.

**Concrete target:** Find stock candidates with a credible shot at +10% return within 15 trading days (스윙 매매). "credible" is defined by measured backtest hit rate, not by reputation of the technique.

**Methodology principle (non-negotiable, explicitly agreed):** No technical pattern (이동평균 교차, 거래량 돌파, RSI/MACD 등) is assumed to work in advance. Each candidate rule must be backtested against real historical KIS data — specifically, measure what fraction of historical signal occurrences were followed by +10%+ within the next 15 trading days — before it's trusted or used for live screening. Gut feel / "well-known technique" framing is explicitly rejected as a substitute for this measurement.

**Why:** User raised this directly: "성공률 높은 주식 기법을 활용하여 15일내 수익률 10%이상 할 수 있는 종목을 찾아내는게 목표". When Claude noted no technique has a-priori guaranteed success, user agreed backtest-driven validation is the way forward ("응 백테스트로 검증하면서 가자").

**How to apply:** Never present a screening rule as good/reliable without a backtest number behind it. When resuming this thread, the natural next blockers are: (1) ~~full KOSPI/KOSDAQ stock master list~~ DONE 2026-07-02 — `stock.item` now has 4,377 rows (KOSPI 2,551 + KOSDAQ 1,826) loaded from KIS's official `kospi_code.mst`/`kosdaq_code.mst` files. Note: this master mixes in ETF/ETN/fund-wrap products (6-digit codes are common stock, but not exclusively — 379 7-digit and 78 9-digit non-common-stock codes are also in there); filtering to actual 보통주 for the real screening universe still needs the KIS master's 증권그룹구분코드 field (part2 of the fixed-width format, not parsed yet — see the 2026-07-02 21:38 note in `/mnt/c/project/stock` for the exact byte-offset spec if resuming this). (2) enough historical daily bars per stock to backtest 15-day-forward returns (currently only ~30 days collected for 2 watchlist items, likely need 1+ year across the real screening universe). (3) an actual backtest harness (given a signal-generation rule + historical data, compute historical hit rate for the +10%/15-day target). Universe size (full ~2,400 real stocks vs. starting with a smaller liquid subset, e.g. by market cap) still undecided.
