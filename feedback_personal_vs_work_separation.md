---
name: feedback-personal-vs-work-separation
description: "At home, the user also does personal tasks (documents, stock data organization) alongside ERP dev work — personal content must never surface during company (dcos) sessions"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 28afaa96-7cdb-44ba-b7f4-6cb6fb5def19
---

At the home PC ([[feedback_seoju_shortcut]] context, `/mnt/c/project/dev/erp`), the user does personal, non-work tasks too — documents/paperwork, organizing stock market data, etc. — in addition to ERP dev work. All memory files sync via the same GitHub `claude_info` repo to both the home and company PCs, so personal-task memories will physically exist on the company machine as well.

**Why:** The user does not want personal/stock-related matters to appear or be referenced while working in the company ([[feedback_dcos_shortcut]], `/mnt/c/IW-DEV`) context. They explicitly chose behavioral separation over technically excluding personal memory files from the git sync (i.e. it's fine that the files co-exist in the repo).

**How to apply:** When operating under the `dcos`/company context, never mention, reference, or act on personal/stock/paperwork-related memories or history — treat that content as out of scope entirely, even though it's technically present in the synced memory folder. Personal topics are only in-scope when the user is working under the `seoju`/home context (or has otherwise clearly signaled they're doing personal, non-ERP work at home).
