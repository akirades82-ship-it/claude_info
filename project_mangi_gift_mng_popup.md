---
name: project-mangi-gift-mng-popup
description: "mangi-gift-mng-popup.vue (만기연장 상품매핑 관리, TB_MEMBER_MANGI_GIFT_MNG CRUD popup) — confirmed fully wired end-to-end as of 2026-07-06"
metadata: 
  node_type: memory
  type: project
  originSessionId: b6ec325d-13a4-43af-b28c-cbe16563113d
---

Working on `work-vsc-2th/powerservice-vue/src/ps5/components/mangi/popup/mangi-gift-mng-popup.vue` — CRUD popup for TB_MEMBER_MANGI_GIFT_MNG (만기연장 상품매핑, expiry-extension product mapping). Table columns: SEQ (NUMBER), INSERT_GBN (VARCHAR2(2)), M_PERIOD_CD (CHAR(3)), GIFT_CODE (VARCHAR2(5)), DEL_FG (CHAR(1)).

As of 2026-07-06 14:41, the Vue file (381 lines) is fairly complete: search form (insert_gbn/m_period_cd/gift_nm), KendoGrid list, read/create/update forms with KendoDropDownList for insert_gbn (code PRD010) and m_period_cd (code PRD021, all periods) and gift_code, validator (`vali_giftmng_save` requiring insert_gbn/m_period_cd/gift_code), and `saveData()`/`createData()`/`editData()` methods following the BaseGrid mixin pattern.

Frontend calls these backend endpoints:
- `/dlw/mangimng/giftmnglist` (grid list, paged, sort reg_dm desc)
- `/dlw/mangimng/insertgiftmng` (create)
- `/dlw/mangimng/updategiftmng` (update, sends org_insert_gbn/org_m_period_cd/org_gift_code as the original-key params)
- `/dlw/mangimng/deletegiftmng` (delete, uses BaseGrid mixin's built-in delete config)
- `/dlw/pay/getMemberMangiGiftset` (dropdown source for active gift codes, called with `{gift_nm: '', ext_period: ''}` — unpaged full list)

Backend (work-eclipse-2th, package `powerservice.business.dlw`) confirmed fully wired end-to-end, no gaps:
- `giftmnglist`/`insertgiftmng`/`updategiftmng`/`deletegiftmng` → `DlwMangiMngController` → `DlwMangiMngServiceImpl` → `DlwMangiMngMapper` → `DlwMangiMngMap.xml`. Delete is a soft-delete (`DEL_FG='Y'` update, not a real DELETE). List query joins `TB_MEMBER_MANGI_GIFT_MNG` with `TB_MEMBER_MANGI_GIFTSET`.
- `getMemberMangiGiftset` (dropdown source) → `DlwPayController` → `DlwPayServiceImpl` → `DlwPayMapper` → `DlwPayMap.xml`, `WHERE DEL_FG='N'` — reads the *related* `TB_MEMBER_MANGI_GIFTSET` table, not `TB_MEMBER_MANGI_GIFT_MNG` itself.

**Why:** Session got disconnected mid-work before this could be checkpointed; recovered by inspecting file mtime/contents directly since git isn't used in these project dirs. Backend wiring was then verified via agent search on 2026-07-06.

**How to apply:** This popup is done end-to-end (frontend + backend) as of 2026-07-06 — no known open work here. If asked to continue "만기연장 상품매핑" work, confirm with the user what remains (e.g. testing, a specific bug) rather than assuming basic CRUD is still unbuilt.
