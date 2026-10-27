# T1 Project Plan

## Project Goal

Develop a clear and reproducible research workflow for comparing three familiar asset classes represented by ETFs: SPY (US equities), TLT (long-term US Treasury bonds), and GLD (gold). The project starts with this written plan in T1; later tutorials reuse the repository to run a bounded analysis task and organize a verifiable agent workflow.

## Available Data

The current dataset is `data/etf_snapshot.csv`, one row per ETF with the columns defined in `data/data_dictionary.md`:

| Ticker | Asset class | Expected return (%) | Volatility (%) | Max drawdown (%) | Expense ratio (%) |
|---|---|---|---|---|---|
| SPY | US Equity | 8.2 | 18 | -24 | 0.09 |
| TLT | Long-Term US Treasury | 4 | 14 | -18 | 0.15 |
| GLD | Gold | 5.5 | 15.5 | -16 | 0.4 |

The dataset is **synthetic teaching data**: all numeric values are illustrative assumptions, not live or historical market observations. Later tutorials introduce instructor-prepared daily price data (`data/t2/`), which is not yet part of this T1 plan.

## Expected Final Deliverable

The final deliverable is a concise written project plan committed as `artifacts/t1/project-plan.md`, reviewed by students and saved with Git. Beyond T1, planned work is expected to produce an analysis report comparing the three ETFs on risk, return, drawdown, and cost; the details are set in later tutorials.

## Three Project Milestones

1. **Plan (T1)**: Create this initial project plan from the repository overview and data dictionary; students review and save it with Git. JiuwenSwarm does not commit or push during T1.
2. **Analysis (T2)**: Planned work — ask an Agent to inspect the prepared daily price data, write and run a small local calculation, verify the result, and produce a comparison report covering expense ratios and maximum drawdowns with peak/trough dates.
3. **Verification and wrap-up**: Planned work — manually check at least one reported drawdown using the source prices and a calculator, review the method's limitations, and save the final report and supporting script for inspection and reruns.

## One Data Limitation

The snapshot is synthetic teaching data; its values are illustrative assumptions rather than current quotations or verified historical estimates. The dataset also omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints, so it is not suitable for investment advice or real investment decisions.

## Next Action

Proceed to the analysis tutorial (T2): inspect the instructor-prepared daily price inputs, ask an Agent to write and run a small local calculation, verify the output, and save the resulting report under `artifacts/t2/`. Before that, students should review this plan and save it with Git.
