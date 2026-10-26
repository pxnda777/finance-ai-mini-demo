# T1 Project Plan

## Project Goal

Develop a clear and reproducible research workflow for comparing three familiar asset classes: SPY (US equities), TLT (long-term US Treasury bonds), and GLD (gold). The project starts with a written plan in T1, and later tutorials will use the same repository to design a bounded analysis task and organize a verifiable agent workflow.

## Available Data

- `data/etf_snapshot.csv` — one illustrative row per ETF (SPY, TLT, GLD) with columns: `ticker`, `asset_class`, `expected_return_pct`, `volatility_pct`, `max_drawdown_pct`, `expense_ratio_pct`.
- `data/data_dictionary.md` — field definitions, units, and the dataset's limitations.

Note: the dataset is synthetic teaching data, not live or historical market observations.

## Expected Final Deliverable

For T1, the deliverable is this concise written plan (`artifacts/t1/project-plan.md`), reviewed and saved with Git. In later tutorials, the final deliverable is planned to be an agent-assisted analysis report that compares the three ETFs, produced from the same repository and verified by the student.

## Three Project Milestones

1. **Project setup (T1)** — create this plan, review it, and save it with Git.
2. **Data analysis (T2)** — planned work: write and run a small local analysis on instructor-prepared daily price data, then verify the results and save a report.
3. **Review and reporting** — planned work: inspect the computed results, document observations and a manual check, and finalize the comparison report.

## One Data Limitation

All numeric values in `etf_snapshot.csv` are synthetic teaching assumptions; they are not current quotations, verified historical estimates, or forecasts, and must not be used as investment advice. The dataset also omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints.

## Next Action

Have this plan reviewed and saved with Git to close out T1; afterwards, proceed to the T2 analysis task using the instructor-prepared daily price data.
