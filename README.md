# Airline PPC Optimization (Portfolio Project)

**Goal:** Maximize revenue (or profit) at a fixed budget by reallocating spend across publisher/match/keyword-group using real PPC metrics.

## Data
Source: `DoubleClick_For_Students` sheet from an airline PPC workbook (provided). Cleaned into `data/clean/ppc_clean.csv` and aggregated to `summary_by_publisher_match_group.csv`.

## KPIs (overall)
- Impressions: 41,868,674
- Clicks: 512,849
- Spend: 755315.92
- Bookings: 3,939
- Revenue: 4661912.55
- CTR: 0.0122
- Avg CPC: 1.4728
- Conversion Rate: 0.0077
- ROAS: 6.1721

## Deliverables
- `data/clean/ppc_clean.csv` – keyword-level cleaned dataset with reconstructed metrics.
- `data/clean/summary_by_publisher_match_group.csv` – grouped rollup (publisher, match type, keyword group).
- `output/recommendations_rule_based.csv` – **increase / decrease / pause / hold** flags with rationale.
- `output/budget_allocation.csv` – heuristic reallocation (bounded 0.5×–1.5×) that keeps total budget fixed.
- `docs/figures/top_roas_groups.png`, `docs/figures/spend_vs_revenue.png` – quick visuals.
- `notebooks/01_eda_and_optimizer.ipynb` – starter notebook to reproduce the analysis.

## Method
1. Recomputed CTR/CPC/CVR/CPA/ROAS from raw clicks, spend, bookings, revenue to ensure consistency.
2. **Rule-based recommendations**: thresholds on ROAS (≥1.2 increase, ≤0.8 decrease), zero-booking pauses, and low-volume holds.
3. **Budget heuristic**: Increased or decreased group spend proportional to (ROAS−1) with 0.5×–1.5× bounds, then rescaled to maintain the current total spend. **Assumption:** local linear response at current ROAS (documented in `notebooks`).

> Note: Without true bid response curves, this allocator is a pragmatic heuristic suitable for a portfolio piece. In practice, you'd calibrate elasticity per keyword and simulate diminishing returns.

## How to run
Open the notebook and run all cells.
- Python 3.x with `pandas`, `numpy`, `matplotlib`, `nbformat` (already used here).
- Update thresholds in `output/recommendations_rule_based.csv` logic if needed.

## Executive takeaway (template)
- Shift budget **from low-ROAS groups to high-ROAS groups** within safe bounds to project **+Δ revenue at flat spend**.
- Pause underperformers with ≥50 clicks and 0 bookings.
- Test higher bids on high-ROAS, high-volume groups (Publisher/Match).

*Generated on 2025-08-14 08:07 UTC.*
