# Finance Data OS

![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)  
![Python](https://img.shields.io/badge/python-3.11%2B-blue.svg)  
![Status](https://img.shields.io/badge/status-active-brightgreen.svg)  
![GitHub stars](https://img.shields.io/github/stars/Si944-byte/finance-data-os?style=social) 

---

## 🚀 Project Goal

To build a **modular financial data platform** that takes raw equities, options, and macroeconomic datasets and transforms them into analytics-ready features for trading and investment research.


---
## 🏗️ Architecture (Phase 1)

<img width="3840" height="275" alt="Untitled diagram _ Mermaid Chart-2025-09-04-222054" src="https://github.com/user-attachments/assets/1f4e8c9c-11aa-4ab3-9618-58c901a8ec2b" />

---

📂 Project Layout

docs/       # architecture diagrams, notes

artifacts/  # Power BI files, exported charts

Build Logs/ # Weekly build logs

notebooks/  # Jupyter notebooks (Week 1, Week 2, etc....)

---

🛣 Project Roadmap

This project is built and shipped in weekly artifacts. Each week delivers a small but meaningful piece of the pipeline.

Week 1 – Single-Ticker Prototype ✅

  - Ingest raw AAPL daily CSV → Parquet

  - Pandera validation + SMA10

  - First Power BI chart (Close vs SMA10)

Week 2 – Multi-Ticker Ingest & Finance Chart ✅

  - Expanded pipeline to handle multiple tickers (AAPL, MSFT, TSLA)

  - Partitioned Parquet outputs

  - Feature engineering (SMA10)

  - Power BI dashboard with:

  - Closing Price vs SMA lines

  - Volume bars on secondary axis

  - Dynamic chart title linked to slicer

  - Clean finance-style formatting

Week 3 – Expanding History & Feature Store ✅

  - Ingest 5+ years of daily OHLCV per ticker (AAPL, MSFT, NVDA, TSLA) via yfinance(auto_adjust=True).

  - Write partitioned Parquet lake: lake/ohlcv/ticker=<T>/year=<YYYY>/<T>_<YYYY>.parquet.

  - Repair pass (idempotent): normalize/rename columns, coerce types, enforce ticker/year consistency.

  - Lake validation: required columns, nulls, numeric types, duplicate (ticker,date), partition checks.

  -  Feature engineering v2:

    return1 (daily % return)

    sma10 (10-day simple moving average)

    vol20 (20-day rolling stdev of close)

  - Ship feature_mart.parquet (single tidy table for BI/analytics).

  - Power BI 3-page dashboard:

    Price vs. SMA10 with KPI cards (Latest Close, Latest SMA10, Close vs SMA10 %).

    Volatility & Distribution — daily return line, vol20 trend with reference lines, histogram of returns.

    Overview/Compare — normalized close (start=1.0), summary table (Avg Return %, Vol, Cumulative Return %, Latest Close, CAGR %, Positive Day %), bar chart with conditional       formatting.

  - DAX measures: Avg Return %, Vol (stdev of return1), Positive Day %, Latest Close, Latest SMA10, Close vs SMA10 %, Cumulative Return %, CAGR %.

  - Date table (DAX) and relationship to fact tables for robust time slicing.

  - Notebook + build log: Week 3 .ipynb and documentation added for reproducibility.

Week 4 – Signals, Backtest & 3-Page Power BI ✅

  - Build Signals Mart

    - Compute sma50 and vol20 (20-day stdev of return1)

    - Create rules: long_rule (sma10 ≥ sma50 & low-vol), exit_rule (sma10 < sma50 or high-vol)

    - Write lake/signals_mart.parquet

  - Implement long-only backtest (next-bar execution)

    - position[t] = long_rule[t-1] → ret_strat = position * return1 → equity = (1+ret_strat).cumprod()

    - Per-ticker daily outputs to lake/backtest_mart/<TICKER>.parquet

    - KPI summary (CAGR, Sharpe, Max DD, Win rate) to lake/backtest_mart/_summary.parquet

  - Power BI model (single-direction relationships, Date as time spine)

    - Ingest full Windows paths to the three parquet sources for reliable refresh

    - Tables: signals_mart, backtest_mart (per-ticker dailies), _summary, existing ohlcv_features, Date, Ticker

  - Dashboards (3 pages)

    - Signals: Closing Price vs SMA50 (50-day) + KPI cards (Latest Close, Latest SMA50, Close vs SMA50 %) and dynamic title

    - Backtest: Strategy Equity Curve, Daily Return distribution, Monthly Return Heatmap

    - Summary: KPI table (CAGR, Sharpe, Max DD, Win rate, Positive Day %, Latest Close, Cumulative Return %), Normalized Close comparison, bar chart with conditional                 formatting on Avg Return %
   
  Week 5 – Costs, Controls & Tuning ✅  

  Objectives

    1. Upgrade signals → Signals v2 (SMA fast/slow + volatility filter).

    2. Run next-bar, after-cost backtest (per-side bps on entry & exit).

    3. Write per-ticker daily files and KPI summary parquet.

    4. Log trades with a simple cost model.

    5. (Optional) Grid tuning across SMA/vol parameters; persist results.

    6. Add sanity checks (schema, dates, KPIs) for reproducibility.

    7. Build/refresh Power BI model & visuals (3 pages).

    8. Ship release notes + artifacts.

---

⚡ Quick Start (Follow along with me!)

1. Clone the repo:

![Quick start](https://github.com/user-attachments/assets/9c55d018-1f03-4d41-94c7-22eef2cbe481)

2. Set up virtual environment:

![virtual environment](https://github.com/user-attachments/assets/6e670fa6-0e35-4667-8baf-138b5d87363d)

3. Install Dependencies:

![dependencies](https://github.com/user-attachments/assets/6fb5db89-88ed-459d-a833-ef7797e57a54)

4. Run the notebooks:

![Jupyter notebook](https://github.com/user-attachments/assets/8ffd40a2-ec9d-4452-ac9a-efad5450b042)


---

📝 Build Logs

Build Log – Week 1
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk1

Build Log – Week 2
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk2

Build Log - Week 3
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk3

Build Log - Week 4
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk4

Build Log - Week 5
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk5

---

🗺️ Week 5 — What's New

Costs, Controls & Tuning

Goal: Produce after-cost strategy returns, KPIs, an optional parameter grid search, and a refreshed Power BI model.

Outputs: (written to lake\)

  signals_mart_v2.parquet — ticker, date, close, sma_fast, sma_slow, vol20, long_rule, exit_rule, regime_low_vol

  backtest_mart_v2\*.parquet — per-ticker dailies: date, ticker, return1, position, ret_after_cost, equity, close

  backtest_mart_v2\_summary.parquet — by-ticker KPIs: CAGR %, Sharpe, Max DD %, Win Rate %

  trades_mart_v1\*.parquet — trade events with cost model fields

  tuning_mart.parquet (optional) — KPI summary per [sma_fast, sma_slow, vol_threshold] combo

How to reproduce:

  1. Open the Week-5 notebook from the repo’s notebooks/ folder.

  2. Run Path Discovery (auto-finds nearest lake\ with expected files).

  3. Run Parameters & Helpers (set SMA/VOL/COST_BPS).

  4. Execute Build Signals v2 → Run Backtest (after-cost).

  5. Execute Trades Log (optional, writes per-ticker parquet).

  6. Execute Tuning (optional grid search; writes tuning_mart.parquet).

  7. Run Sanity Checks (shape, columns, KPIs within tolerance).

  8.In Power BI, connect to:
   backtest_mart_v2\_summary.parquet
   Folder backtest_mart_v2\ (per-ticker dailies)
   signals_mart_v2.parquet
   (Optional) tuning_mart.parquet

  9. Confirm model relationships: Date[Date] → * single-direction, Ticker[ticker] → * single-direction to each mart.

  10. Create/refresh measures (DAX) using this week’s ingests:
    Daily Return = SUM(backtest_mart_v2[ret_after_cost])
    Equity (cum) via PRODUCTX over selected dates
    Cumulative Return % = [Equity (cum)] - 1
    CAGR % using years = DISTINCTCOUNT('Date'[Date]) / 252
    Sharpe (annual) = AVERAGEX(...) / STDEVX.P(...) * SQRT(252)
    Win Rate % = COUNTROWS(Return>0) / COUNTROWS(Date)
    Max DD % (running high vs equity; returns negative %)
    Latest Close = VAR lastDate = MAX('Date'[Date]) RETURN CALCULATE(MAX(backtest_mart_v2[close]), 'Date'[Date] = lastDate)

Notes & assumptions:
  
  - Next-bar execution; per-side COST_BPS charged on both entry and exit
  - No dividends/fees/borrow modeled unless in source price; no slippage beyond fixed bps
  - Results are illustrative; use for research only
---

### 🧠 What I Learned

**Week 1 – Single-Ticker Prototype**  
- Learned what a **Parquet file** is: a columnar storage format optimized for analytics.  
- Unlike CSV, Parquet is **compressed, faster to query, and schema-aware**, which makes it essential when dealing with **large amounts of financial data**.  
- Saw firsthand how partitioned Parquet reduces storage size and improves performance when scaling beyond one ticker.  

**Week 2 – Multi-Ticker Ingest & Finance Chart**  
- Learned how to extend the pipeline to **multiple tickers** and why partitioning by `ticker` and `year` is critical for efficient querying.  
- Discovered how **Pandera schema validation** enforces data quality rules before the data moves downstream — preventing “bad data” from entering the feature store.  
- Understood how to compute **technical indicators** like SMA (Simple Moving Average) and **returns**, which are core to financial analysis.  
- Improved skills in **Power BI visualization**: building combo charts, formatting axes, and designing finance-ready dashboards that balance clarity and detail. (really focused on cleaning up the charts this week)
  
**Week 3 – Expanding History & Feature Store**  
- Adjusted vs. unadjusted prices: Using yfinance(auto_adjust=True) means the Close is already split/dividend‐adjusted, so there’s no need for an Adj_Close column. This removed a whole class of schema errors.
- Idempotent “repair pass” pays off: A small, re-runnable step that re-coerces types, fills missing ticker, and trims rows to the folder’s ticker/year makes the lake reliable and easy to fix if something goes wrong.
- Partition consistency matters: Validating that file paths (e.g., ticker=MSFT/year=2024) agree with row values (ticker and date.year) catches subtle mistakes early.
- Rolling features need alignment guards: Rolling windows and % change can misalign indexes; explicitly resetting index and checking equal lengths avoids silent drift.
- Cumulative Return vs. CAGR:
    Cumulative Return % = total growth over the selected period (product of daily returns − 1).
    CAGR % = the annualized growth rate across the same period, which makes different date ranges comparable.
- Date table = better time intelligence: A proper DAX Date table with one-to-many relationships enables consistent slicers, % by year/month, and avoids filter ambiguity.
- Power BI modeling tricks:
    Dynamic titles with SELECTEDVALUE improve clarity.
    Rule-based conditional formatting draws attention to outliers (e.g., highest Avg Return %).
    Reference lines (e.g., 20% vol) and consistent axes make charts easier to read across tickers.
- “Feature Mart” is a contract: Finalizing a tidy, validated feature_mart.parquet (date, ticker, close, return1, sma10, vol20) simplifies downstream analytics and BI.
- Small design polish matters: Finance-style cards, subtle gridlines, neutral palette, and consistent units (%, USD) improve perceived quality without extra compl

**Week 4 – Signals, Backtest & 3-Page Power BI** 
- Next-bar execution prevents look-ahead.
Shifting signals by one day (position[t] = signal[t-1]) keeps the backtest honest and reproducible.
- A dedicated Signals Mart simplifies BI.
Precomputing MAs/volatility and boolean rules in parquet keeps the report fast and the DAX minimal.
- Date is the hub. Using a single Date table with one-way filters into each fact table eliminates circular filters and odd totals.
- KPIs you can trust. Simple, transparent formulas (CAGR from daily equity, Sharpe from daily mean/stdev, Max DD via running peak) + sanity checks (end equity ≈ product of returns) caught mistakes early.
- Visual clarity beats clever markers. Scatter markers for every buy/exit look noisy at daily granularity; price + SMA lines with KPI cards tell the story better.
- Operational detail matters. Importing parquet via full file paths on Windows made refresh reliable; consistent formatting (decimals, % signs) made the report feel “finished.”
- Small UX touches help. Dynamic page titles (ticker + date range) and a Reset bookmark improve readability and exploration

**Week 5 – Costs, Controls, Tuning & Power BI** 
1) Paths & environments must be bulletproof.
We hit “file not found” due to a stray notebooks\lake\ and mixed slashes. Fix: a robust path discovery helper that walks parents to the first folder that actually contains expected parquet names, and loudly warns if a shadow lake exists under notebooks.
2) Respect your schema contract—but be tolerant.
Columns varied between steps (ret_after_cost vs earlier names). The loader now:
  - Prefers in-memory per_ticker_daily when available (same session).
  - Else reads parquet excluding _summary, accepting common column variants, then normalizes to date, ticker, return1, position.
3) Small API clarity prevents big breakage.
Errors like “trades_from_position not defined” came from mismatched cell ordering/names. We centralized helpers (build_signals_v2, run_backtest_with_costs, kpi, load_per_ticker_daily) and called them consistently.
4) Grid search pitfalls.
The initial tuning loop threw “too many values to unpack” and undefined GRID_FAST. Resolution: define grid lists up front; use a single nested loop (for f in GRID_FAST / for s in GRID_SLOW / for v in GRID_VOL) and return KPI() per combo. Keep the function pure (input fm → output summary rows).
5) Sanity checks save time.
A couple asserts caught issues early: date parsing, empty tables, KPI drift (CAGR mismatch). For single-element Series, cast with .iloc[0] to avoid future pandas warnings.
6) DAX should mirror the data you actually ingested.
  -We removed references to nonexistent columns (e.g., sma50, rev_strat), anchored measures to Week-5 fields, and fixed:
    - Latest Close using lastDate = MAX('Date'[Date]) then CALCULATE(MAX(backtest_mart_v2[close]), 'Date'[Date] = lastDate).
    - Monthly heatmap: diverging CF center = 0.00, Month sorted by Month Number.
7) Modeling discipline in Power BI.
Kept single-direction relationships (Date/Ticker → facts) to avoid filter ambiguity. The Normalized Close issue for AAPL was traced to filtering/measure scope; verifying ALLSELECTED context and slicers fixed it.
8) UX polish matters.
Consistent number formats, legible line weights, clean slicers, and concise cards made the 3 pages read clearly. Heatmap totals and centered color scale improved interpretation at a glance.

Main issues this week (and how we solved them)

❌ Lake paths resolving to notebooks\lake → ✅ parent-walk path discovery + warning if duplicate lake exists.

❌ Missing parquet columns / name drift → ✅ tolerant loader + normalized column names.

❌ Undefined helpers / variable names (per_ticker_daily, GRID_FAST) → ✅ consolidated helper section + explicit grid lists.

❌ Grid tuning “too many values to unpack” → ✅ simplified nested loops; return KPI summary rows.

❌ KPI assert mismatch (Series casting) → ✅ use .iloc[0] and numeric casts.

❌ DAX measures referring to non-ingested fields → ✅ measures rewritten to Week-5 fields only (e.g., ret_after_cost, close).

❌ Normalized Close missing one ticker → ✅ check slicers/filters, ensure measure uses proper filter context, confirm Date–Ticker relationships.
---

### 🗂️ Artifacts (Week 4: current week)

Power BI Dashboard: 



---

🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

