---
name: feedback-default-email-recipient
description: "When the user just says '이메일 보내줘' (send an email) without specifying a recipient, default to akirades@naver.com"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

The user's standing default email recipient is **akirades@naver.com** (a Naver address, separate from their akirades82@gmail.com account). Content/subject isn't fixed — only the destination is a standing default.

**Why:** User said nothing else about email is decided yet, but whenever they ask to send an email without naming a recipient, it should go here.

**How to apply:** When the user says something like "이메일 보내줘" with no recipient specified, use akirades@naver.com unless they explicitly name a different address for that particular email. Still confirm subject/content with them before actually sending, since only the recipient is fixed by default. Note: as of 2026-07-02 no email-sending mechanism (SMTP/API) is configured in this environment yet — see whatever note/setup follows this one for how sending is actually implemented once decided.
