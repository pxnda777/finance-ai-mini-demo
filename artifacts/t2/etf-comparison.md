# T2 ETF Comparison: Annual Fees and Maximum Drawdown (SPY, TLT, GLD)

This report continues the T1 written plan (artifacts/t1/project-plan.md) and upgrades it from the synthetic one-row snapshot to real, instructor-prepared daily price data, comparing SPY, TLT and GLD on disclosed annual fees and the maximum drawdown actually observed in the supplied price window.

## Sources and setup

- **Inputs:** `data/t2/daily_prices.csv` (7,536 daily observations), `data/t2/fund_info.csv` (3 fund records), `data/t2/data_dictionary.md` (field definitions). `artifacts/t1/project-plan.md` was used for context only; every numeric claim below comes from the T2 pack.
- **Pack:** T2 ETF Data Pack, prepared on 2026-09-25; historical source recorded as Yahoo Finance chart API downloaded on 2026-09-20.
- **Drawdown window:** common window 2016-09-01 through 2026-08-31 (inclusive), daily session frequency (US market sessions; weekends and full-day closures absent), using the `adjusted_close` column, which reflects the provider's split and dividend-distribution adjustments. The `close` column was retained for inspection only.
- **Fee disclosure dates (as recorded in `fund_info.csv`, fee recheck date 2026-09-25):**
  - SPY: fund-information as-of date 2026-09-10; fee-specific effective date **not stated** (gross of waivers/reimbursements).
  - TLT: current prospectus; specific date **not stated** in the fee panel.
  - GLD: effective date **not stated** in the selected field.
- **Script:** `artifacts/t2/calculate_drawdown.py`; executed with `python3 artifacts/t2/calculate_drawdown.py` (Python 3.9.6, standard library only).
- **Input checks (before calculation):** all passed — exactly 3 tickers (SPY, TLT, GLD); 7,536 unique ticker/date pairs (no duplicates); 2,512 rows per ETF; dates ascending within each ticker; all `close`/`adjusted_close` values positive and finite; common first date 2016-09-01 and common last date 2026-08-31; identical date sets across the three tickers. Nothing was dropped or filled.
- **Calculation method:** for each ticker, all `adjusted_close` observations in the window with a cumulative maximum from the window start: `drawdown_t_pct = (adjusted_close_t / high_t - 1) * 100`, where `high_t` is the largest adjusted close observed from the window start through day t; the maximum drawdown is the minimum of `drawdown_t_pct`. Ties select the earliest trough and its earliest corresponding peak; with no loss, the first date is used for both dates with zero drawdown. Full precision was kept internally; only display is rounded to two decimals.

## 1. Comparison

| Ticker | Annual expense ratio (%) | Maximum drawdown (%) | Peak date | Trough date |
|---|---:|---:|---|---|
| SPY | 0.0945 | -33.72 | 2020-02-19 | 2020-03-23 |
| TLT | 0.15 | -48.35 | 2020-08-04 | 2023-10-19 |
| GLD | 0.4 | -26.40 | 2026-01-29 | 2026-07-16 |

Fee precision is preserved as disclosed (0.0945%, 0.15%, 0.4%); drawdowns are displayed to two decimals. Peak is on or before trough in every row. These disclosed fees are current disclosure snapshots, not ten-year average fees over the price window; these drawdowns are period measures within 2016-09-01–2026-08-31, not all-time measures.

## 2. Observation

The ETF with the smallest drawdown loss (closest to zero) in this period is **GLD at -26.40%**, followed by SPY at -33.72% and TLT at -48.35%. Drawdowns are non-positive, so closer to zero means a smaller loss magnitude. These values were calculated from `adjusted_close` in this exercise, not read from a precomputed snapshot, and the displayed two-decimal comparison has no ties. Limitation: these are daily-close drawdowns within a fixed historical window and do not measure intraday losses, all-time risk, or future performance.

## 3. Agent Check (self-check by the same Agent)

- **ETF chosen:** SPY.
- **Source rows re-read from `data/t2/daily_prices.csv`** (ticker=SPY):
  - `2020-02-19` adjusted_close=`307.6394958496094`
  - `2020-03-23` adjusted_close=`203.91189575195312`
- **Check command (local, standard library):** a Python heredoc that reads `daily_prices.csv` with `csv.DictReader`, keeps the SPY rows, and recomputes `(trough / peak - 1) * 100` from the two reported dates.
- **Actual output:** `RECOMPUTE (trough/peak-1)*100 = -33.7172572108% (rounded: -33.72%)`; `MATCH: YES`. Method review on the full 2,512-row SPY series: cumulative maximum adjusted close up to 2020-03-23 is 307.6394958496 on 2020-02-19 (the reported peak); peak date is before the trough date; the minimum adjusted close in [2020-02-19, 2020-03-23] equals the trough price 203.9118957520; all adjusted closes are positive and dates are ascending.
- **Comparison:** the recomputed value matches the report's full-precision value (-33.7172572108%) and its two-decimal display (-33.72%). No correction or recheck was needed.
- **Observation cross-check:** comparing all three displayed results, GLD (-26.40%) is closest to zero, then SPY (-33.72%), then TLT (-48.35%); no ties, consistent with Section 2.
- This is the Agent's own self-check of its calculation; it is not independent verification, and the student has not re-checked the data.
