# KisClient API 구현 로드맵 (Top 20)

- 기준 데이터: `OPEN_TRADING_API_GAP_LIST.csv` (missing 항목)
- 선정 방식: 주문/잔고/체결/가능수량 중심 가중치 스코어링
- 목적: 실거래 운영에 필요한 API부터 단계적으로 확장

## 1) 우선순위 Top 20

1. `domestic_stock` / `order_resv_rvsecncl` / `/uapi/domestic-stock/v1/trading/order-resv-rvsecncl`
2. `domestic_stock` / `order_resv_ccnl` / `/uapi/domestic-stock/v1/trading/order-resv-ccnl`
3. `overseas_stock` / `daytime_order_rvsecncl` / `/uapi/overseas-stock/v1/trading/daytime-order-rvsecncl`
4. `domestic_stock` / `pension_inquire_psbl_order` / `/uapi/domestic-stock/v1/trading/pension/inquire-psbl-order`
5. `overseas_stock` / `order_rvsecncl` / `/uapi/overseas-stock/v1/trading/order-rvsecncl`
6. `overseas_stock` / `order_resv_ccnl` / `/uapi/overseas-stock/v1/trading/order-resv-ccnl`
7. `domestic_futureoption` / `order_rvsecncl` / `/uapi/domestic-futureoption/v1/trading/order-rvsecncl`
8. `domestic_futureoption` / `inquire_psbl_order` / `/uapi/domestic-futureoption/v1/trading/inquire-psbl-order`
9. `domestic_futureoption` / `inquire_psbl_ngt_order` / `/uapi/domestic-futureoption/v1/trading/inquire-psbl-ngt-order`
10. `overseas_futureoption` / `order_rvsecncl` / `/uapi/overseas-futureoption/v1/trading/order-rvsecncl`
11. `domestic_stock` / `order_resv` / `/uapi/domestic-stock/v1/trading/order-resv`
12. `domestic_stock` / `order_credit` / `/uapi/domestic-stock/v1/trading/order-credit`
13. `overseas_stock` / `daytime_order` / `/uapi/overseas-stock/v1/trading/daytime-order`
14. `domestic_stock` / `inquire_psbl_rvsecncl` / `/uapi/domestic-stock/v1/trading/inquire-psbl-rvsecncl`
15. `overseas_stock` / `order_resv_list` / `/uapi/overseas-stock/v1/trading/order-resv-list`
16. `overseas_stock` / `order_resv` / `/uapi/overseas-stock/v1/trading/order-resv`
17. `overseas_stock` / `order` / `/uapi/overseas-stock/v1/trading/order`
18. `overseas_futureoption` / `inquire_daily_order` / `/uapi/overseas-futureoption/v1/trading/inquire-daily-order`
19. `domestic_stock` / `pension_inquire_present_balance` / `/uapi/domestic-stock/v1/trading/pension/inquire-present-balance`
20. `domestic_stock` / `pension_inquire_balance` / `/uapi/domestic-stock/v1/trading/pension/inquire-balance`

## 2) 단계별 구현 계획

### Phase 1 - 주문/계좌 핵심 (8)
1. `domestic_stock` / `order_resv_rvsecncl`
   - path: `/uapi/domestic-stock/v1/trading/order-resv-rvsecncl`
   - 목적: 주식예약주문정정취소
2. `domestic_stock` / `order_resv_ccnl`
   - path: `/uapi/domestic-stock/v1/trading/order-resv-ccnl`
   - 목적: 주식예약주문조회
3. `overseas_stock` / `daytime_order_rvsecncl`
   - path: `/uapi/overseas-stock/v1/trading/daytime-order-rvsecncl`
   - 목적: 해외주식 미국주간정정취소
4. `domestic_stock` / `pension_inquire_psbl_order`
   - path: `/uapi/domestic-stock/v1/trading/pension/inquire-psbl-order`
   - 목적: 퇴직연금 매수가능조회
5. `overseas_stock` / `order_rvsecncl`
   - path: `/uapi/overseas-stock/v1/trading/order-rvsecncl`
   - 목적: 해외주식 정정취소주문
6. `overseas_stock` / `order_resv_ccnl`
   - path: `/uapi/overseas-stock/v1/trading/order-resv-ccnl`
   - 목적: 해외주식 예약주문접수취소
7. `domestic_futureoption` / `order_rvsecncl`
   - path: `/uapi/domestic-futureoption/v1/trading/order-rvsecncl`
   - 목적: 선물옵션 정정취소주문
8. `domestic_futureoption` / `inquire_psbl_order`
   - path: `/uapi/domestic-futureoption/v1/trading/inquire-psbl-order`
   - 목적: 선물옵션 주문가능

### Phase 2 - 파생/해외 확장 (6)
1. `domestic_futureoption` / `inquire_psbl_ngt_order`
   - path: `/uapi/domestic-futureoption/v1/trading/inquire-psbl-ngt-order`
   - 목적: (야간)선물옵션 주문가능 조회
2. `overseas_futureoption` / `order_rvsecncl`
   - path: `/uapi/overseas-futureoption/v1/trading/order-rvsecncl`
   - 목적: 해외선물옵션 정정취소주문
3. `domestic_stock` / `order_resv`
   - path: `/uapi/domestic-stock/v1/trading/order-resv`
   - 목적: 주식예약주문
4. `domestic_stock` / `order_credit`
   - path: `/uapi/domestic-stock/v1/trading/order-credit`
   - 목적: 주식주문(신용)
5. `overseas_stock` / `daytime_order`
   - path: `/uapi/overseas-stock/v1/trading/daytime-order`
   - 목적: 해외주식 미국주간주문
6. `domestic_stock` / `inquire_psbl_rvsecncl`
   - path: `/uapi/domestic-stock/v1/trading/inquire-psbl-rvsecncl`
   - 목적: 주식정정취소가능주문조회

### Phase 3 - 시세/분석 보강 (6)
1. `overseas_stock` / `order_resv_list`
   - path: `/uapi/overseas-stock/v1/trading/order-resv-list`
   - 목적: 해외주식 예약주문조회
2. `overseas_stock` / `order_resv`
   - path: `/uapi/overseas-stock/v1/trading/order-resv`
   - 목적: 해외주식 예약주문접수
3. `overseas_stock` / `order`
   - path: `/uapi/overseas-stock/v1/trading/order`
   - 목적: 해외주식 주문
4. `overseas_futureoption` / `inquire_daily_order`
   - path: `/uapi/overseas-futureoption/v1/trading/inquire-daily-order`
   - 목적: 해외선물옵션 일별 주문내역
5. `domestic_stock` / `pension_inquire_present_balance`
   - path: `/uapi/domestic-stock/v1/trading/pension/inquire-present-balance`
   - 목적: 퇴직연금 체결기준잔고
6. `domestic_stock` / `pension_inquire_balance`
   - path: `/uapi/domestic-stock/v1/trading/pension/inquire-balance`
   - 목적: 퇴직연금 잔고조회

## 3) 구현 규칙 (현재 정책 반영)

- 주문 API(`order*`, `*rvsecncl`)는 기존 `Primary-Only` 가드 경유 필수
- 조회 API는 다계좌 분산 구조와 충돌 없도록 클라이언트별 분리 유지
- 신규 API는 `GetAsync/PostAsync` 경로를 `OPEN_TRADING_API_GAP_LIST.csv`와 1:1 매핑
- 완료 시 `tools/generate_openapi_gap_list.py` 재실행으로 수치 갱신

## 4) 완료 기준

- [x] Top 20 일부 API 메서드 시그니처 추가 (2026-03-02)
- [x] 요청/응답 모델 추가 및 deserialize 검증 (순위분석 DTO 반영)
- [x] 주문 계열 Primary-Only 정책 단위 검증 (국내/해외 주문 계열 반영 완료)
- [x] 갭 문서 재생성 후 Implemented 수치 증가 확인 (`Implemented=27`)

## 5) 2026-03-02 진행 현황

- 완료 API(Top20 연계)
   - `domestic_stock/order_resv`
   - `domestic_stock/order_resv_rvsecncl`
   - `domestic_stock/order_resv_ccnl`
   - `domestic_stock/pension_inquire_psbl_order`
   - `domestic_stock/pension_inquire_present_balance`
   - `domestic_stock/pension_inquire_balance`
   - `domestic_stock/inquire_psbl_rvsecncl`
   - `overseas_stock/daytime_order`
   - `overseas_stock/daytime_order_rvsecncl`
   - `overseas_stock/order_resv`
   - `overseas_stock/order_resv_ccnl`
   - `domestic_futureoption/order_rvsecncl`
   - `domestic_futureoption/inquire_psbl_order`
- 추가 반영(요청 기반)
   - 국내주식 순위분석 4종 구현 + UI Ranking 탭 연결