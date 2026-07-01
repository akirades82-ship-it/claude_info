---
name: frontend-backend-mapping
description: "How the 5 backend Tomcat modules map to Vue frontend builds/pages, including which modules have no Vue UI"
metadata: 
  node_type: memory
  type: project
  originSessionId: b164312e-7833-4fdf-949c-6f78fe62fc3c
---

Mapping between the 5 backend modules (Tomcat instances in `work-eclipse-2th/Servers/`) and the Vue frontend (`work-vsc-2th/powerservice-vue`), per [[project_scope_and_stack]]:

| Backend module (Tomcat) | Frontend |
|---|---|
| powerservice (`1.ps5-config`) | Vue `serve:ps5`/`build:ps5` — pages: login, user, admin, walb, popup |
| partner (`2.pp-config`) | Vue `serve:pp`/`build:pp` — pages: login, admin, walb, popup, rdcs |
| receipt (`4.rect-config`) | Vue `serve:rc`/`build:rc` — pages: recp(웹접수) |
| wallboard (`3.walb-config`) | **No Vue.** Served directly as its own plain JSP app (`wallboard/webapp/index.jsp`, `script/iwws.js`) |
| billing (`5.bill-config`) | **No frontend at all.** Pure OpenAPI backend for PG (payment gateway) integrations — `billing/webapp/openapi/` has per-provider folders (nicepay, kcb, opengiro, readycash, etc.), tied to the SDKs in `lib/nicepay`, `lib/okname`, `lib/petra` |

Important nuance confirmed by user: the `walb` page that appears *inside* the ps5 and pp Vue builds (전광판, titled the same as "wallboard") is a **separate, distinct screen** from the wallboard module's own standalone JSP app — they are not the same UI served two ways. Don't conflate them.

**Why:** Came up when auditing what "프론트/백 서버 정리" covers — needed to confirm whether the wallboard-titled page embedded in ps5/pp Vue builds was actually proxying/duplicating the wallboard module's JSP app.

**How to apply:** When asked about wallboard-related frontend work, clarify whether the user means the JSP app under `wallboard/webapp/` or the `walb` page inside ps5/pp Vue builds — they are unrelated screens despite the shared name. When asked about billing, don't look for a Vue UI for it — it's API-only.
