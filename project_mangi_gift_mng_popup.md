---
name: project-mangi-gift-mng-popup
description: "In-progress dev on mangi-gift-mng-popup.vue (만기연장 상품매핑 관리, TB_MEMBER_MANGI_GIFT_MNG CRUD popup)"
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

**Why:** Session got disconnected mid-work before this could be checkpointed; recovered by inspecting file mtime/contents directly since git isn't used in these project dirs.

**How to apply:** Next step was verifying/building the Java backend (work-eclipse-2th) — controller, service, DAO, MyBatis mapper XML — for the 5 endpoints above, and confirming table TB_MEMBER_MANGI_GIFT_MNG exists in Oracle. If resuming this work, check backend wiring status first before assuming it's done.
