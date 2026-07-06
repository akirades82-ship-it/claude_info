---
name: feedback-incremental-memory-saves
description: "Save meaningful progress/decisions to memory as they happen during a session, not only at the end — sessions can disconnect unexpectedly and unsaved work is lost"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: b6ec325d-13a4-43af-b28c-cbe16563113d
---

Write memory updates at natural checkpoints during a work session (after finishing a sub-task, after a decision, after finding/fixing a bug) instead of batching everything for a wrap-up at the end.

**Why:** A session was cut off unexpectedly mid-work, and the work done before the disconnect was lost because it hadn't been written to memory yet. The user expected that if progress had been saved incrementally, it would have been recoverable via a "마지막 작업" (last work) query in the next session.

**How to apply:** This applies broadly across contexts (dcos/ERP work, seoju project, any multi-step task), not just [[feedback_seoju_auto_journal]]'s dated-note habit. When doing non-trivial work that spans multiple steps or tool calls, don't wait for the user to ask "저장해줘" or for the conversation to naturally end — checkpoint state (what was done, what's left, what was decided and why) into the relevant project/feedback memory file as you go. Still commit+push per [[reference_memory_git_backup]] after each save, not just once at session end.
