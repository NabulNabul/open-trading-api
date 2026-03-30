# open-trading-api 대비 KisClient 구현 갭 목록

- 비교 기준: `MCP/Kis Trading MCP/configs/*.json`의 `api_path` vs `KisClient/**/*.cs`의 `GetAsync/PostAsync` 경로
- open-trading-api API 수: **166**
- KisClient 매칭 구현 수: **27**
- 미구현(또는 경로 불일치) 수: **139**

## 0) 최근 구현 하이라이트

- 2026-03-02: 국내주식 순위분석 핵심 4종 구현 반영
  - `/uapi/domestic-stock/v1/quotations/volume-rank`
  - `/uapi/domestic-stock/v1/ranking/fluctuation`
  - `/uapi/domestic-stock/v1/ranking/market-cap`
  - `/uapi/domestic-stock/v1/ranking/volume-power`
- 2026-03-02: `KisStockTrading` Ranking 탭 추가 및 더블클릭 일봉 조회 연결

## 1) 툴별 요약

| Tool | Total | Implemented | Missing |
|---|---:|---:|---:|
| auth | 2 | 0 | 2 |
| domestic_bond | 14 | 0 | 14 |
| domestic_futureoption | 20 | 2 | 18 |
| domestic_stock | 74 | 21 | 53 |
| elw | 1 | 0 | 1 |
| etfetn | 2 | 0 | 2 |
| overseas_futureoption | 19 | 0 | 19 |
| overseas_stock | 34 | 4 | 30 |

## 2) 현재 매칭된 API (구현 확인)

### domestic_futureoption (2)
- `inquire_psbl_order` → `/uapi/domestic-futureoption/v1/trading/inquire-psbl-order`
- `order_rvsecncl` → `/uapi/domestic-futureoption/v1/trading/order-rvsecncl`

### domestic_stock (21)
- `fluctuation` → `/uapi/domestic-stock/v1/ranking/fluctuation`
- `inquire_asking_price_exp_ccn` → `/uapi/domestic-stock/v1/quotations/inquire-asking-price-exp-ccn`
- `inquire_balance` → `/uapi/domestic-stock/v1/trading/inquire-balance`
- `inquire_ccnl` → `/uapi/domestic-stock/v1/quotations/inquire-ccnl`
- `inquire_daily_ccld` → `/uapi/domestic-stock/v1/trading/inquire-daily-ccld`
- `inquire_daily_itemchartprice` → `/uapi/domestic-stock/v1/quotations/inquire-daily-itemchartprice`
- `inquire_daily_price` → `/uapi/domestic-stock/v1/quotations/inquire-daily-price`
- `inquire_price` → `/uapi/domestic-stock/v1/quotations/inquire-price`
- `inquire_psbl_order` → `/uapi/domestic-stock/v1/trading/inquire-psbl-order`
- `inquire_psbl_rvsecncl` → `/uapi/domestic-stock/v1/trading/inquire-psbl-rvsecncl`
- `market_cap` → `/uapi/domestic-stock/v1/ranking/market-cap`
- `order_cash` → `/uapi/domestic-stock/v1/trading/order-cash`
- `order_resv` → `/uapi/domestic-stock/v1/trading/order-resv`
- `order_resv_ccnl` → `/uapi/domestic-stock/v1/trading/order-resv-ccnl`
- `order_resv_rvsecncl` → `/uapi/domestic-stock/v1/trading/order-resv-rvsecncl`
- `order_rvsecncl` → `/uapi/domestic-stock/v1/trading/order-rvsecncl`
- `pension_inquire_balance` → `/uapi/domestic-stock/v1/trading/pension/inquire-balance`
- `pension_inquire_present_balance` → `/uapi/domestic-stock/v1/trading/pension/inquire-present-balance`
- `pension_inquire_psbl_order` → `/uapi/domestic-stock/v1/trading/pension/inquire-psbl-order`
- `volume_power` → `/uapi/domestic-stock/v1/ranking/volume-power`
- `volume_rank` → `/uapi/domestic-stock/v1/quotations/volume-rank`

### overseas_stock (4)
- `daytime_order` → `/uapi/overseas-stock/v1/trading/daytime-order`
- `daytime_order_rvsecncl` → `/uapi/overseas-stock/v1/trading/daytime-order-rvsecncl`
- `order_resv` → `/uapi/overseas-stock/v1/trading/order-resv`
- `order_resv_ccnl` → `/uapi/overseas-stock/v1/trading/order-resv-ccnl`

## 3) 미구현 API 목록

### auth (2)
- `auth_token` | `/oauth2/tokenP`
- `auth_ws_token` | `/oauth2/Approval`

### domestic_bond (14)
- `avg_unit` | `/uapi/domestic-bond/v1/quotations/avg-unit`
- `buy` | `/uapi/domestic-bond/v1/trading/buy`
- `inquire_asking_price` | `/uapi/domestic-bond/v1/quotations/inquire-asking-price`
- `inquire_balance` | `/uapi/domestic-bond/v1/trading/inquire-balance`
- `inquire_ccnl` | `/uapi/domestic-bond/v1/quotations/inquire-ccnl`
- `inquire_daily_ccld` | `/uapi/domestic-bond/v1/trading/inquire-daily-ccld`
- `inquire_daily_price` | `/uapi/domestic-bond/v1/quotations/inquire-daily-price`
- `inquire_price` | `/uapi/domestic-bond/v1/quotations/inquire-price`
- `inquire_psbl_order` | `/uapi/domestic-bond/v1/trading/inquire-psbl-order`
- `inquire_psbl_rvsecncl` | `/uapi/domestic-bond/v1/trading/inquire-psbl-rvsecncl`
- `issue_info` | `/uapi/domestic-bond/v1/quotations/issue-info`
- `order_rvsecncl` | `/uapi/domestic-bond/v1/trading/order-rvsecncl`
- `search_bond_info` | `/uapi/domestic-bond/v1/quotations/search-bond-info`
- `sell` | `/uapi/domestic-bond/v1/trading/sell`

### domestic_futureoption (18)
- `display_board_top` | `/uapi/domestic-futureoption/v1/quotations/display-board-top`
- `exp_price_trend` | `/uapi/domestic-futureoption/v1/quotations/exp-price-trend`
- `inquire_asking_price` | `/uapi/domestic-futureoption/v1/quotations/inquire-asking-price`
- `inquire_balance` | `/uapi/domestic-futureoption/v1/trading/inquire-balance`
- `inquire_balance_settlement_pl` | `/uapi/domestic-futureoption/v1/trading/inquire-balance-settlement-pl`
- `inquire_balance_valuation_pl` | `/uapi/domestic-futureoption/v1/trading/inquire-balance-valuation-pl`
- `inquire_ccnl` | `/uapi/domestic-futureoption/v1/trading/inquire-ccnl`
- `inquire_ccnl_bstime` | `/uapi/domestic-futureoption/v1/trading/inquire-ccnl-bstime`
- `inquire_daily_amount_fee` | `/uapi/domestic-futureoption/v1/trading/inquire-daily-amount-fee`
- `inquire_daily_fuopchartprice` | `/uapi/domestic-futureoption/v1/quotations/inquire-daily-fuopchartprice`
- `inquire_deposit` | `/uapi/domestic-futureoption/v1/trading/inquire-deposit`
- `inquire_ngt_balance` | `/uapi/domestic-futureoption/v1/trading/inquire-ngt-balance`
- `inquire_ngt_ccnl` | `/uapi/domestic-futureoption/v1/trading/inquire-ngt-ccnl`
- `inquire_price` | `/uapi/domestic-futureoption/v1/quotations/inquire-price`
- `inquire_psbl_ngt_order` | `/uapi/domestic-futureoption/v1/trading/inquire-psbl-ngt-order`
- `inquire_time_fuopchartprice` | `/uapi/domestic-futureoption/v1/quotations/inquire-time-fuopchartprice`
- `ngt_margin_detail` | `/uapi/domestic-futureoption/v1/trading/ngt-margin-detail`
- `order` | `/uapi/domestic-futureoption/v1/trading/order`

### domestic_stock (53)
- `chk_holiday` | `/uapi/domestic-stock/v1/quotations/chk-holiday`
- `comp_program_trade_daily` | `/uapi/domestic-stock/v1/quotations/comp-program-trade-daily`
- `daily_loan_trans` | `/uapi/domestic-stock/v1/quotations/daily-loan-trans`
- `daily_short_sale` | `/uapi/domestic-stock/v1/quotations/daily-short-sale`
- `estimate_perform` | `/uapi/domestic-stock/v1/quotations/estimate-perform`
- `foreign_institution_total` | `/uapi/domestic-stock/v1/quotations/foreign-institution-total`
- `frgnmem_pchs_trend` | `/uapi/domestic-stock/v1/quotations/frgnmem-pchs-trend`
- `frgnmem_trade_trend` | `/uapi/domestic-stock/v1/quotations/frgnmem-trade-trend`
- `inquire_account_balance` | `/uapi/domestic-stock/v1/trading/inquire-account-balance`
- `inquire_balance_rlz_pl` | `/uapi/domestic-stock/v1/trading/inquire-balance-rlz-pl`
- `inquire_credit_psamount` | `/uapi/domestic-stock/v1/trading/inquire-credit-psamount`
- `inquire_daily_indexchartprice` | `/uapi/domestic-stock/v1/quotations/inquire-daily-indexchartprice`
- `inquire_daily_overtimeprice` | `/uapi/domestic-stock/v1/quotations/inquire-daily-overtimeprice`
- `inquire_daily_trade_volume` | `/uapi/domestic-stock/v1/quotations/inquire-daily-trade-volume`
- `inquire_elw_price` | `/uapi/domestic-stock/v1/quotations/inquire-elw-price`
- `inquire_index_daily_price` | `/uapi/domestic-stock/v1/quotations/inquire-index-daily-price`
- `inquire_index_price` | `/uapi/domestic-stock/v1/quotations/inquire-index-price`
- `inquire_investor` | `/uapi/domestic-stock/v1/quotations/inquire-investor`
- `inquire_investor_daily_by_market` | `/uapi/domestic-stock/v1/quotations/inquire-investor-daily-by-market`
- `inquire_investor_time_by_market` | `/uapi/domestic-stock/v1/quotations/inquire-investor-time-by-market`
- `inquire_member` | `/uapi/domestic-stock/v1/quotations/inquire-member`
- `inquire_member_daily` | `/uapi/domestic-stock/v1/quotations/inquire-member-daily`
- `inquire_overtime_asking_price` | `/uapi/domestic-stock/v1/quotations/inquire-overtime-asking-price`
- `inquire_overtime_price` | `/uapi/domestic-stock/v1/quotations/inquire-overtime-price`
- `inquire_period_profit` | `/uapi/domestic-stock/v1/trading/inquire-period-profit`
- `inquire_period_trade_profit` | `/uapi/domestic-stock/v1/trading/inquire-period-trade-profit`
- `inquire_price_2` | `/uapi/domestic-stock/v1/quotations/inquire-price-2`
- `inquire_psbl_sell` | `/uapi/domestic-stock/v1/trading/inquire-psbl-sell`
- `inquire_time_dailychartprice` | `/uapi/domestic-stock/v1/quotations/inquire-time-dailychartprice`
- `inquire_time_indexchartprice` | `/uapi/domestic-stock/v1/quotations/inquire-time-indexchartprice`
- `inquire_time_itemchartprice` | `/uapi/domestic-stock/v1/quotations/inquire-time-itemchartprice`
- `inquire_time_itemconclusion` | `/uapi/domestic-stock/v1/quotations/inquire-time-itemconclusion`
- `inquire_time_overtimeconclusion` | `/uapi/domestic-stock/v1/quotations/inquire-time-overtimeconclusion`
- `inquire_vi_status` | `/uapi/domestic-stock/v1/quotations/inquire-vi-status`
- `intgr_margin` | `/uapi/domestic-stock/v1/trading/intgr-margin`
- `intstock_multprice` | `/uapi/domestic-stock/v1/quotations/intstock-multprice`
- `intstock_stocklist_by_group` | `/uapi/domestic-stock/v1/quotations/intstock-stocklist-by-group`
- `invest_opbysec` | `/uapi/domestic-stock/v1/quotations/invest-opbysec`
- `invest_opinion` | `/uapi/domestic-stock/v1/quotations/invest-opinion`
- `investor_program_trade_today` | `/uapi/domestic-stock/v1/quotations/investor-program-trade-today`
- `investor_trade_by_stock_daily` | `/uapi/domestic-stock/v1/quotations/investor-trade-by-stock-daily`
- `investor_trend_estimate` | `/uapi/domestic-stock/v1/quotations/investor-trend-estimate`
- `news_title` | `/uapi/domestic-stock/v1/quotations/news-title`
- `order_credit` | `/uapi/domestic-stock/v1/trading/order-credit`
- `pension_inquire_daily_ccld` | `/uapi/domestic-stock/v1/trading/pension/inquire-daily-ccld`
- `pension_inquire_deposit` | `/uapi/domestic-stock/v1/trading/pension/inquire-deposit`
- `period_rights` | `/uapi/domestic-stock/v1/trading/period-rights`
- `program_trade_by_stock` | `/uapi/domestic-stock/v1/quotations/program-trade-by-stock`
- `program_trade_by_stock_daily` | `/uapi/domestic-stock/v1/quotations/program-trade-by-stock-daily`
- `psearch_result` | `/uapi/domestic-stock/v1/quotations/psearch-result`
- `psearch_title` | `/uapi/domestic-stock/v1/quotations/psearch-title`
- `search_info` | `/uapi/domestic-stock/v1/quotations/search-info`
- `search_stock_info` | `/uapi/domestic-stock/v1/quotations/search-stock-info`

### elw (1)
- `volume_rank` | `/uapi/elw/v1/ranking/volume-rank`

### etfetn (2)
- `inquire_price` | `/uapi/etfetn/v1/quotations/inquire-price`
- `nav_comparison_trend` | `/uapi/etfetn/v1/quotations/nav-comparison-trend`

### overseas_futureoption (19)
- `daily_ccnl` | `/uapi/overseas-futureoption/v1/quotations/daily-ccnl`
- `inquire_asking_price` | `/uapi/overseas-futureoption/v1/quotations/inquire-asking-price`
- `inquire_ccld` | `/uapi/overseas-futureoption/v1/trading/inquire-ccld`
- `inquire_daily_ccld` | `/uapi/overseas-futureoption/v1/trading/inquire-daily-ccld`
- `inquire_daily_order` | `/uapi/overseas-futureoption/v1/trading/inquire-daily-order`
- `inquire_deposit` | `/uapi/overseas-futureoption/v1/trading/inquire-deposit`
- `inquire_period_ccld` | `/uapi/overseas-futureoption/v1/trading/inquire-period-ccld`
- `inquire_period_trans` | `/uapi/overseas-futureoption/v1/trading/inquire-period-trans`
- `inquire_price` | `/uapi/overseas-futureoption/v1/quotations/inquire-price`
- `inquire_psamount` | `/uapi/overseas-futureoption/v1/trading/inquire-psamount`
- `inquire_time_futurechartprice` | `/uapi/overseas-futureoption/v1/quotations/inquire-time-futurechartprice`
- `inquire_unpd` | `/uapi/overseas-futureoption/v1/trading/inquire-unpd`
- `margin_detail` | `/uapi/overseas-futureoption/v1/trading/margin-detail`
- `opt_asking_price` | `/uapi/overseas-futureoption/v1/quotations/opt-asking-price`
- `opt_price` | `/uapi/overseas-futureoption/v1/quotations/opt-price`
- `order` | `/uapi/overseas-futureoption/v1/trading/order`
- `order_rvsecncl` | `/uapi/overseas-futureoption/v1/trading/order-rvsecncl`
- `search_contract_detail` | `/uapi/overseas-futureoption/v1/quotations/search-contract-detail`
- `search_opt_detail` | `/uapi/overseas-futureoption/v1/quotations/search-opt-detail`

### overseas_stock (30)
- `algo_ordno` | `/uapi/overseas-stock/v1/trading/algo-ordno`
- `dailyprice` | `/uapi/overseas-price/v1/quotations/dailyprice`
- `foreign_margin` | `/uapi/overseas-stock/v1/trading/foreign-margin`
- `industry_theme` | `/uapi/overseas-price/v1/quotations/industry-theme`
- `inquire_algo_ccnl` | `/uapi/overseas-stock/v1/trading/inquire-algo-ccnl`
- `inquire_asking_price` | `/uapi/overseas-price/v1/quotations/inquire-asking-price`
- `inquire_balance` | `/uapi/overseas-stock/v1/trading/inquire-balance`
- `inquire_ccnl` | `/uapi/overseas-stock/v1/trading/inquire-ccnl`
- `inquire_daily_chartprice` | `/uapi/overseas-price/v1/quotations/inquire-daily-chartprice`
- `inquire_nccs` | `/uapi/overseas-stock/v1/trading/inquire-nccs`
- `inquire_paymt_stdr_balance` | `/uapi/overseas-stock/v1/trading/inquire-paymt-stdr-balance`
- `inquire_period_profit` | `/uapi/overseas-stock/v1/trading/inquire-period-profit`
- `inquire_period_trans` | `/uapi/overseas-stock/v1/trading/inquire-period-trans`
- `inquire_present_balance` | `/uapi/overseas-stock/v1/trading/inquire-present-balance`
- `inquire_psamount` | `/uapi/overseas-stock/v1/trading/inquire-psamount`
- `inquire_search` | `/uapi/overseas-price/v1/quotations/inquire-search`
- `inquire_time_indexchartprice` | `/uapi/overseas-price/v1/quotations/inquire-time-indexchartprice`
- `inquire_time_itemchartprice` | `/uapi/overseas-price/v1/quotations/inquire-time-itemchartprice`
- `order` | `/uapi/overseas-stock/v1/trading/order`
- `order_resv_list` | `/uapi/overseas-stock/v1/trading/order-resv-list`
- `order_rvsecncl` | `/uapi/overseas-stock/v1/trading/order-rvsecncl`
- `period_rights` | `/uapi/overseas-price/v1/quotations/period-rights`
- `price` | `/uapi/overseas-price/v1/quotations/price`
- `price_detail` | `/uapi/overseas-price/v1/quotations/price-detail`
- `price_fluct` | `/uapi/overseas-stock/v1/ranking/price-fluct`
- `quot_inquire_ccnl` | `/uapi/overseas-price/v1/quotations/inquire-ccnl`
- `rights_by_ice` | `/uapi/overseas-price/v1/quotations/rights-by-ice`
- `search_info` | `/uapi/overseas-price/v1/quotations/search-info`
- `trade_vol` | `/uapi/overseas-stock/v1/ranking/trade-vol`
- `updown_rate` | `/uapi/overseas-stock/v1/ranking/updown-rate`

## 4) 참고

- 상세 원본(전체 상태)은 `OPEN_TRADING_API_GAP_LIST.csv` 참고
- 본 결과는 경로 문자열 기반 정적 비교이므로, 동일 기능이 다른 경로/래퍼로 구현된 경우 수동 검증 필요