---
name: feedback-backtest-before-verbal-risk-claims
description: "In the seoju stock project, don't voice gut-feel risk/caution commentary about a candidate that isn't backed by a backtest — it contradicts the tool's own ranking and confuses the user"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 4681e82b-b5fb-4193-92ff-1d1b752798c9
---

In [[project_stock_screening_goal]], this project's core discipline is "no technical pattern is trusted without a measured backtest." That discipline applies to Claude's own conversational risk commentary too, not just code/rules — don't say things like "this looks risky because it already ran up a lot" unless it's actually been tested against history.

**Why:** On 2026-07-07, Claude warned that S-Oil being up +9% on its signal day made it more vulnerable to a pullback if bought the next day — a plausible-sounding but untested claim. The user pushed back: the system ranks S-Oil as a top candidate while Claude verbally undercuts that same recommendation with an unverified caution — "이렇게 이야기 해주는데 추천해주면 혼란이 있잖아" (this creates confusion). When actually backtested (`/api/backtest/momentum-split`), the claim was not just unsupported but backwards — bigger same-day moves predicted *higher* hit rates, roughly monotonically. This is the same mistake the project has already guarded against for code (rejected heuristics: institutional-accumulation, rsi-oversold-bounce, volatility-contraction, PersistentStableRule) — Claude just made the verbal version of it.

**How to apply:** Before adding a cautionary or confidence-boosting comment about a candidate that isn't already backed by an existing validated rule/flag (stopLossPrc, gappedDown, macroPenalty, signalDayReturnPct, etc.), either (a) don't say it, or (b) if it seems worth checking, propose backtesting it first (cheap to do — momentum-split-style bucket analysis pattern is already built and reusable) rather than asserting it as fact. If a hypothesis is validated, wire it into the actual ranking/UI (as was done with signalDayReturnPct) so the tool and the commentary stay consistent — don't leave validated findings as spoken-only asides.
