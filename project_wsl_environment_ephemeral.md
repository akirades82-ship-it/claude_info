---
name: project-wsl-environment-ephemeral
description: "This WSL/Linux environment (Postgres + myerp backend/frontend) used to only run while a Claude Code session was connected; as of 2026-07-02 it's set up to auto-boot at Windows logon and stay up independently"
metadata:
  type: project
  originSessionId: 4b2319be-253b-4561-856b-5058082548d1
---

Originally confirmed 2026-07-02 (morning): system `uptime` and the `postgresql` systemd service's start timestamp matched exactly — this Linux environment only booted when a Claude Code session connected, so anything inside it (Postgres, any future batch) went down between sessions.

**Fixed 2026-07-02 (evening):** WSL has `systemd=true` in `/etc/wsl.conf`, and once systemd's init (PID 1) is running it doesn't exit, so the WSL2 VM itself stays up indefinitely once booted — it just needed something to trigger the initial boot outside of Claude Code. Set up:
- `postgresql.service` — already `systemctl enable`d (unchanged).
- `myerp-backend.service` / `myerp-frontend.service` — new systemd units, `enable`d, in `/etc/systemd/system/`. See [[project_stock_feature_progress]] for what they run.
- Windows Task Scheduler task `WSL-AutoStart-Ubuntu` (`schtasks /Create ... /SC ONLOGON`) to boot the `Ubuntu` WSL distro at Windows login, so nothing needs to open a WSL terminal or Claude Code for it to be running. **Could not be created via WSL interop** (Korean Windows username breaks `schtasks.exe` argument encoding when invoked cross-boundary from WSL) — has to be run natively in a Windows PowerShell/CMD window; confirm with the user whether they've done this before assuming the box is truly always-on.

**How to apply:** Don't assume this constraint still fully applies — check `systemctl status myerp-backend myerp-frontend postgresql` and whether the Windows scheduled task exists before concluding something is/isn't running. If the Windows-side scheduled task was never completed by the user, the environment (and everything in it) still only comes up when a WSL terminal or Claude Code session starts it, same as before.
