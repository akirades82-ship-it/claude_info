---
name: db-config-reference
description: "Where DB connection config lives for the Java backend, and what DB types are in play"
metadata: 
  node_type: memory
  type: reference
  originSessionId: b164312e-7833-4fdf-949c-6f78fe62fc3c
---

DB connection settings (datasource URLs/users, NOT stored here for security) for the Java backend live at:

`work-eclipse-2th/powerservice/src/main/resources/egovframework/egovProps/globals-DEV.properties`

(eGovFrame-based config. Confirmed: every module — `powerservice`, `partner`, `billing`, `wallboard`, `receipt` — has 3 profile files side by side: `globals-DEV.properties`, `globals-TST.properties`, `globals-PRD.properties`.)

Main DB currently in active use: **Oracle 19c only** (user-confirmed), driven via `oracle.jdbc.driver.OracleDriver`. Multiple named Oracle datasources exist for different downstream systems, e.g. `ps5`, `cau`, `dmlifeweb`, `dlwmall`, `dmnewhome`, `nexcore`. The `raps` (MySQL) and `gocs` (PostgreSQL) datasources defined in the DEV properties are **not currently used** — leftover/inactive config, not live integrations.

**PRD (production) is off-limits for autonomous action.** `globals-PRD.properties` holds real production DB credentials/endpoints. User explicitly said: do not auto-connect to, or execute anything against, the PRD side.

**Why:** User pointed to the DEV properties file as the place to check DB config. The file(s) contain live credentials, so those must never be copied into memory or logs. Separately, user flagged PRD as production and does not want any automatic connection/execution targeting it — specifically because instructions (from the user or ambiguous requests) can contain mistakes, and a mistaken command hitting production is much higher-consequence than one hitting DEV/TST. The safeguard has to hold even when a request sounds like it's asking for PRD action, unless it's unambiguous and explicit in the moment.

**How to apply:** When DB connection details are needed, Read the relevant `globals-DEV.properties` directly rather than assuming from memory (credentials rotate). Never persist passwords/keys from these files into memory, chat summaries, or committed docs. Never run, connect, deploy, or execute anything against `globals-PRD.properties` targets or any PRD-configured environment without explicit, in-the-moment user instruction — treat this as a hard stop, not just a default to avoid.
