---
name: feedback-respond-in-korean
description: "User writes in Korean and expects replies in Korean, not English"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 137d2d63-6912-466c-947b-fdaa77035766
---

User corrected 2026-07-06 ("한글로 알려줘야지" — "you should tell me in Korean") after a fully English response to a Korean question about the seoju stock-screening project.

**Why:** User writes to Claude in Korean and expects the conversation to stay in Korean, at least in the seoju ([[feedback_seoju_shortcut]]) context. Code, identifiers, and technical terms can stay in English as needed, but prose/explanation/analysis should default to Korean.

**How to apply:** Default to responding in Korean for this user unless they write in English or ask for English. Applies at least to seoju/home sessions; treat as the general default unless a dcos/company-session norm proves otherwise.
