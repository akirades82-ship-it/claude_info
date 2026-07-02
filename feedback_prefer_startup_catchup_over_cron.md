---
name: feedback-prefer-startup-catchup-over-cron
description: "In this session-bound WSL environment, prefer 'catch up on next startup' logic over fixed-time cron/@Scheduled jobs for any periodic task — the box isn't reliably up at a given clock time"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 4b2319be-253b-4561-856b-5058082548d1
---

When building any periodic/scheduled behavior inside the seoju home WSL environment (or apps running in it, like myerp-backend), default to "check state on startup and catch up if behind" rather than a fixed-time cron trigger (`@Scheduled`, systemd timer at a specific hour, etc.).

**Why:** This WSL box only runs when something actually starts it (a Claude Code session, a manual WSL open, or — if ever set up — Windows Task Scheduler at logon; see [[project_wsl_environment_ephemeral]]). A fixed-time trigger like "daily 16:00 KST" silently never fires on any day the box wasn't up at that exact moment, which is the common case, not the exception. User caught this directly: first attempt at daily stock-data collection used a 16:00 cron job, and the user pointed out it'd be more reliable to just backfill missing data whenever a session connects. Implemented as `StartupCatchUpRunner` (Spring `ApplicationRunner`) in `myerp-backend` — checks `MAX(trade_dt)` vs today, backfills the gap if behind, no-ops if already current.

**How to apply:** Before adding any `@Scheduled`/cron-style job in this environment, ask whether "run once at each startup, catch up on the gap" would work just as well — it usually will, and it's strictly more robust here since it doesn't depend on the box's uptime schedule at all. Reserve real cron/fixed-time triggers for cases where the *exact* timing genuinely matters (rare for a personal batch/reporting job), not as the default.
