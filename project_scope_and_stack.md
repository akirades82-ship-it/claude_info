---
name: project-scope-and-stack
description: "Which folders to use for actual project work in /mnt/c/IW-DEV, and the tech stack (Vue frontend, Java backend)"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: b164312e-7833-4fdf-949c-6f78fe62fc3c
---

When working in `/mnt/c/IW-DEV`, only treat **2_WORKS**, **files**, and **lib** as relevant for source/reference. The other top-level folders (1_IDES, 3_UTILS, 4_INSTALLS, 5_DEPLOY) are installer/tool dumps, not project content.

- **2_WORKS** — actual source code workspaces. Only the `-2th` variants are current/active:
  - `work-vsc-2th`: Vue frontend (`powerservice-vue`, yarn-based) — open/edited with **VS Code**
  - `work-eclipse-2th`: Java backend, Maven multi-module Eclipse workspace (modules: `billing`, `partner`, `powerservice`, `receipt`, `wallboard`), Spring-based (`.springBeans` present) — open/edited with **Eclipse**, run locally as 5 separate Tomcat server instances under `work-eclipse-2th/Servers/`, one per module:
    - `1.ps5-config` → powerservice
    - `2.pp-config` → partner
    - `3.walb-config` → wallboard
    - `4.rect-config` → receipt
    - `5.bill-config` → billing
  - `work-vsc` and `work-eclipse` (non `-2th`) are older copies — ignore unless user explicitly asks for them
- **files** — reference/shared files (gongje, home, sftp_home)
- **lib** — external SDKs/libraries (nicepay, okname, petra) and setup scripts

**Why:** User explicitly said the root folder mixes installers, source code, and reference material, so only these three folders should be searched/referenced going forward. Then narrowed further: within 2_WORKS, only the `-2th` workspaces are relevant. Confirmed stack: Vue (frontend, VS Code) + Java (backend/server, Eclipse).

**How to apply:** Default file searches and exploration to `2_WORKS/work-vsc-2th`, `2_WORKS/work-eclipse-2th`, `files`, `lib` instead of scanning the whole `/mnt/c/IW-DEV` root or the non-2th workspaces. When asked about frontend code, look under `2_WORKS/work-vsc-2th`; for backend/server code, look under `2_WORKS/work-eclipse-2th`. When discussing running/debugging the backend, remember it's 5 independently-running local Tomcat instances (one per module, see mapping above), not a single combined server.
