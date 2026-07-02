---
name: feedback-auto-proceed-no-blocker
description: "When there's no real blocker/risk, don't pause to ask 'should I proceed?' — just continue with reasonable judgment and report what was done"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 4b2319be-253b-4561-856b-5058082548d1
---

Stop asking "진행할까요?" / "이어서 할까요?" as a routine checkpoint between steps of an already-agreed-upon task (e.g. mid-flow in the seoju stock screening work). Only pause to explicitly check in when there's a genuine blocker: a real ambiguous decision with meaningful tradeoffs the user would want to weigh in on, a risky/destructive/hard-to-reverse action, or something technically failed and needs their input to resolve.

**Why:** User said directly: "실질적으로 내가 너가 하고 있는 무언가를 중간에 체크한다는게 어려워서" — checking in on what Claude is doing mid-task is impractical for them in this kind of exploratory/iterative work, so repeated "proceed?" prompts are friction, not helpfulness. This came up during the seoju stock screening project after several rounds of Claude pausing between natural next-steps to ask permission.

**How to apply:** For open-ended "what's next" forks within a direction the user has already set (e.g. "build the live candidate detector" vs "explore more rules" — both are reasonable continuations of the same agreed goal), just pick the more sensible one and proceed, then report results. Reserve actual questions for: security/destructive actions (already covered by the general safety instructions), a choice where the user's personal preference genuinely can't be inferred (e.g. UI/aesthetic taste), or when something breaks and needs a human call. Don't treat "which of two reasonable next steps" as one of those cases.
