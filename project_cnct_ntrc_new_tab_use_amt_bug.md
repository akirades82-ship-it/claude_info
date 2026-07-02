---
name: project-cnct-ntrc-new-tab-use-amt-bug
description: "Known unfixed bug in cnct-ntrc-new-tab.vue saveData()/setSaveParam(): shopping_use_amt saved from stale custInfo.use_amt instead of live-refreshed custInfo.ready_cash"
metadata: 
  node_type: memory
  type: project
  originSessionId: 6338ba3e-9c78-41da-9e0c-0e86924794d4
---

In `work-vsc-2th/powerservice-vue/src/ps5/components/user/main/popup/cnct-rgsn-tabs/cnct-ntrc-new-tab.vue` (part of [[project_scope_and_stack]]'s Vue frontend, 해약접수(NEW) tab), `saveData()` (line 816) and `setSaveParam()` (line 1001) both do:

```js
oSelected.shopping_use_amt = oCustInfo.use_amt;
```

`custInfo.use_amt` and `custInfo.ready_cash` are both set to the same initial value when the popup loads, via `DlwResnReceiptController.java` `/accnt-new-info` (work-eclipse-2th, lines 217-218: `mAccnt.put("ready_cash", sReadyCash); mAccnt.put("use_amt", sReadyCash);`). But if the user later clicks "조회" in the sibling 환급정보 tab (`cnct-dtpt-tab.vue`, `searchReadyCash()` line 434-449), only `custInfo.ready_cash` gets refreshed with the new value from `/dlw/readycash/amount/use/list` — `custInfo.use_amt` is never updated again. So saving after that refresh persists the stale initial value instead of the corrected one.

Older sibling file `cnct-rgsn-tab.vue:732` does this correctly, referencing `oCustInfo.ready_cash` instead of `use_amt` in the equivalent spot — confirms `use_amt` is the wrong field to read here.

**Why:** Found while investigating a user-reported error in how `saveData()`'s referenced values relate to the `getReceiptAccntNewInfo` MyBatis query (`DlwResnReceiptMap.xml`). The query itself and most `custInfo` fields line up fine; this `use_amt`/`ready_cash` desync was the one real defect, and it's a staleness bug (multiple async populators of the same store object), not a param-name mismatch.

**How to apply:** As of 2026-07-02, the fix (replace `oCustInfo.use_amt` with `oCustInfo.ready_cash` at lines 816 and 1001 of `cnct-ntrc-new-tab.vue`) had been proposed but not yet applied. If asked about this bug again, check whether the fix has already landed (git blame / read the current file) before re-investigating from scratch. More generally: in this popup family, `cnctStore.custInfo` is populated by multiple independent async calls (initial tab load + per-tab refresh buttons), so duplicate/derived fields can silently go out of sync — worth checking for this pattern in similar bug reports involving `cnctStore.custInfo`.
