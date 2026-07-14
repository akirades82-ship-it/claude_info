---
name: project-daytrading-pivot
description: "2026-07-14: seoju stock project pivoted from swing (15-day/+15%) to day-trading (단타, next-day intraday ~5% target) after the swing observation sample came back 6 STOPPED / 0 HIT; auto order execution explicitly left UNDECIDED, not approved"
metadata: 
  node_type: memory
  type: project
  originSessionId: eaadd277-09e4-4c0e-a984-73f1b647fa1a
---

Confirmed 2026-07-14, right after finalizing the swing observation-mode sample: [[project_stock_screening_goal]]'s 07-06~07-13 코스닥 라이브 신호 8건이 STOPPED 6 / PENDING 2 / **HIT 0**으로 마감됐고, 그 직후 사용자가 방향 전환을 제안했다.

**Confirmed via 3 explicit questions (do not re-derive from vibes — these were asked directly because they touch a prior hard boundary):**

1. **스윙 → 단타 완전 전환.** [[project_stock_screening_goal]]의 15일/+15% 스윙 스레드는 보류(관찰 모드 자체는 살아있지만 신규 개발 중단). 지금부터 신규 개발은 단타(익일 당일 매매) 대상.
2. **자동 매수/매도 주문 실행은 "아직 결정 안 함"** — 명시적으로 미확정 상태로 남겨둠. 이것은 2026-07-02 [[project_stock_feature_progress]]에 적힌 "KIS 주문 API(매수/매도) 연동 절대 금지" 원칙이 뒤집혔다는 뜻이 **아니다.** 로직/백테스트가 먼저이고, 실제 주문 자동화 여부는 나중에 별도로 다시 확인받아야 한다.
3. **실행 인프라는 별도 호스팅서버에 신규 구축** (현재 WSL의 myerp/스윙용 인프라와는 분리). 다만 지금 당장 필요한 결정은 아니고 로직 설계 이후의 문제.

**단타 컨셉 (사용자 설명):**
전일(D-1) 데이터로 익일(D) 단타 후보 종목을 미리 선별 → D일 09시 이후 "매수 자리"에서 매수 → 매수 시점에 손절가/익절가를 미리 계산해 세팅 → 자동(또는, 자동 여부 미정이므로 결국은 수동일 수도) 매도. 목표는 스윙보다 낮은, 전일 기준 약 +5% 정도. **수수료(매수/매도 수수료 + 매도 시 증권거래세)를 반드시 감안해서 손절/익절가를 계산해야 한다**고 사용자가 직접 강조 — 마진이 스윙보다 훨씬 타이트해서 수수료가 중요한 변수.

**Why:** 스윙 전략이 실측 데이터(하락장 8건 표본)에서 edge를 보여주지 못한 상태에서 사용자가 새 방향을 제안했고, 동시에 그동안 지켜온 "주문 자동화 절대 금지" 원칙을 건드리는 요청이라 설계 착수 전에 명시적으로 확인부터 받았다.

**수수료/세금 확정 (2026-07-14):** 거래수수료 0.147%(편도, 매수/매도 각각) + 증권거래세·농특세 합산 0.20%(매도 시에만) → 왕복 총비용 약 0.494%. 손절/익절가 계산은 반드시 이 수치를 반영 (+5% 익절 목표 시 수수료 제외 순익 약 +4.51%; 손절 -X%면 실손실은 X%+0.494%). 이 수치는 사용자가 직접 확인해 준 실제 값이므로 추측치로 덮어쓰지 말 것.

**분봉 정밀 시뮬레이션 1차 결과 (2026-07-14):** stock.price_minute 테이블 + KIS 주식일별분봉조회(TR FHKST03010230) 연동 완료. daytrade-strongclose-2.0x-3(코스닥) 최근 200신호(2026-04~07)로 즉시매수/갭확인후진입/ORB 3방식 x 손절 2~7%를 수수료 반영 정밀검증: **즉시매수는 전 구간 순손실로 확정적으로 나쁨. "갭확인후진입(09:00~09:05 방향 확인, 역행시 스킵)+넓은 손절(5~7%)"만 유일하게 일관된 플러스(+0.2~0.76%, 손절폭 여러 값에서 안정적이라 커브피팅 가능성 낮음)**. 단, 표본이 한 시기(대부분 하락장)에 몰려있고 out-of-sample 검증 전이라 아직 신뢰 확정 단계 아님. 상세: `/mnt/c/project/stock/20260714_211217_pivot_swing_to_daytrading_decided.txt`.

**How to apply:** 
- 단타 스크리닝/백테스트 로직 설계는 바로 진행해도 되지만, **KIS 주문(매수/매도) API를 실제로 연동하는 코드는 사용자가 다시 한번 명시적으로 승인하기 전엔 작성하지 말 것.** "로직부터 보자"는 대답을 승인으로 착각하지 말 것.
- [[project_stock_screening_goal]]의 "기법은 백테스트로 검증되기 전엔 신뢰 안 함" 원칙을 단타에도 동일 적용 — 눌림목/갭/거래량 등 어떤 진입 패턴이든 과거 분봉 데이터로 승률을 실측한 뒤에 채택.
- 정확한 수수료율/거래세율은 추측하지 말고 사용자에게 실제 계좌 기준 수치를 확인받을 것 — [[feedback_backtest_before_verbal_risk_claims]]와 같은 맥락(근거 없는 손익 주장 금지).
- 진행 경위 상세는 `/mnt/c/project/stock/20260714_211217_pivot_swing_to_daytrading_decided.txt` 참고.
