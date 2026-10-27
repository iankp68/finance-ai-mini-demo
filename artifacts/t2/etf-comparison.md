# T2 ETF Comparison Report

Dataset: **T2 ETF Data Pack** (instructor-prepared classroom data)
Preparation date: **2026-09-25**
Historical window: **2016-09-01 through 2026-08-31** (inclusive), 2,512 daily observations per ETF
Inputs used: `data/t2/daily_prices.csv` and `data/t2/fund_info.csv` (unchanged)
Calculation script: `artifacts/t2/drawdown_calc.py`

## Input Checks (executed before calculation)

All checks passed; no rows were dropped or filled.

- Tickers: SPY, TLT, GLD — PASS
- Unique ticker/date pairs: 7,536 unique of 7,536 rows — PASS
- Rows per ETF = 2,512: SPY=2512, TLT=2512, GLD=2512 — PASS
- Ascending dates within each ticker — PASS
- Positive finite `close` — PASS
- Positive finite `adjusted_close` — PASS
- Equal date sets across tickers — PASS
- Common first date 2016-09-01 and common last date 2026-08-31 — PASS

## 1. Comparison

Annual expense ratios are issuer disclosures recorded on 2026-09-25, in percentage units with source precision preserved. Maximum drawdowns were calculated from `adjusted_close` (not from `close` and not read from a precomputed snapshot), kept at full precision during calculation, and displayed to two decimal places.

| Ticker | Annual expense ratio (%) | Max drawdown (%) | Peak date | Trough date |
|---|---|---|---|---|
| SPY | 0.0945 | -33.72 | 2020-02-19 | 2020-03-23 |
| TLT | 0.15 | -48.35 | 2020-08-04 | 2023-10-19 |
| GLD | 0.4 | -26.40 | 2026-01-29 | 2026-07-16 |

## 2. Observation

GLD has the smallest drawdown loss (closest to zero) in this period, at **-26.40%**, compared with SPY at -33.72% and TLT at -48.35%. There are no ties among the displayed two-decimal results. Drawdowns were calculated from `adjusted_close`, not read from a precomputed snapshot; they are non-positive, and closer to zero means a smaller loss magnitude.

One limitation: this measures daily-close drawdown within the fixed historical window only; it does not measure intraday losses, all-time risk, or future performance, and the disclosed fees are current disclosure snapshots (as of 2026-09-25), not ten-year average fees.

## 3. Agent Check

This is the Agent's own self-check; it is not independent verification and no student manually checked the data.

**Chosen ETF: GLD** (the observation winner).

**Source rows re-read from `data/t2/daily_prices.csv`:**

| Date | Ticker | close | adjusted_close |
|---|---|---|---|
| 2026-01-29 | GLD | 495.8999938965 | 495.8999938965 |
| 2026-07-16 | GLD | 364.9599914551 | 364.9599914551 |

**Check command:** `python artifacts/t2/agent_check_gld.py`

**Actual output (abridged):**
```text
Two-point recompute (trough/peak - 1)*100 = -26.4045178570% (display -26.40%)
Full-series recompute: max drawdown -26.4045178570% (display -26.40%)
  peak 2026-01-29 (495.8999938965) -> trough 2026-07-16 (364.9599914551)
Peak-before-trough order: PASS
Full-series pair matches reported pair: PASS
```

**Comparison:** The two-point formula `(trough / peak - 1) * 100` on the re-read source values gives **-26.4045178570%** (display **-26.40%**), identical to the reported GLD value. An independent full-series recompute over all 2,512 GLD dates (cumulative high from window start, minimum drawdown, earliest extrema on ties, peak on or before trough) returns the same pair and value, so the two-point arithmetic is consistent with the window minimum, not merely a local pair.

**Method review:** The calculation inspected all dates and `adjusted_close` values, tracked cumulative highs from the window start, enforced peak-before-trough ordering, and compared the observation across all three ETFs (GLD -26.40% closest to zero; no ties). A two-point check alone cannot prove a pair is the worst in the whole window; the full-series recompute covers that gap.

**Correction/recheck:** While drafting, a first version of the observation logic selected the most negative drawdown instead of the closest-to-zero value. The logic was corrected to compare the maximum (closest to zero) drawdown, the script was rerun, and all displayed results were rechecked. No input files were modified.
