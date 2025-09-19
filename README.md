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

notebooks/  # Jupyter notebooks (Week 1, Week 2, Week 3…)

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

---

🗺️ Week 4 — What's New

1) Make a “signals” dataset (when to be in or out)

  SMA50: the average closing price over the last 50 days. It smooths the price line.

  Vol20: the typical day-to-day wiggle over the last 20 days (a basic volatility number).

Rules

  Go long (be in the stock) when the short average (SMA10) is above the long average (SMA50) and volatility is low.

  Exit (be out) when SMA10 falls below SMA50 or volatility is high.

  Save this table as a file: lake/signals_mart.parquet.

  Why: This gives Power BI a clean, ready-to-use table that says “buy” or “exit” each day.

2) Do a simple backtest (see how that rule would have done)

  “Next-day” rule: If yesterday said “go long,” we enter today. If yesterday said “exit,” we get out today. (Prevents cheating by using future info.)

  Daily strategy return:

  If we’re in the position, it equals the stock’s daily return.

  If we’re out, it’s zero.

  Equity curve: Start at $1.00 and grow it by the daily strategy returns to see how the account would have changed over time.

  Save results:

  One file per ticker with daily equity etc.: lake/backtest_mart/<TICKER>.parquet

  A summary table with key stats (KPIs): lake/backtest_mart/_summary.parquet

  CAGR = average yearly growth

  Sharpe = return compared to volatility (higher is better)

  Max Drawdown = worst peak-to-valley drop (more negative is worse)

  Win rate = % of up days while in the trade

  Why: This shows if the rule adds value vs. buy-and-hold.

3) Connect everything in Power BI

  Import the three parquet files using the full Windows paths so refresh is reliable.

  Tables in the model:

  Date (drives time), Ticker (AAPL/MSFT/…), ohlcv_features (prices & features),

  signals_mart (buy/exit info), backtest_mart (daily strategy equity), _summary (KPIs).

  Use one-way relationships from Date (and Ticker) into the other tables. Date is the “spine.”

  Why: Keeps filtering simple and avoids model glitches.

4) Build the 3 report pages

  Page 1 — Signals

  Line chart: Close price vs SMA50 (50-day).

  KPI cards: Latest Close, Latest SMA50, Close vs SMA50 %.

  Dynamic title: shows selected ticker + date range.

  Page 2 — Backtest

  Equity curve (how $1 grew under the rule).
  
  Histogram of daily strategy returns.

  Monthly return heatmap (which months/years were strong or weak).

  Page 3 — Summary

  KPI table: CAGR, Sharpe, Max DD, Win rate, Positive Day %, Latest Close, Cumulative Return %.

  Normalized Close comparison (all tickers start at 1.0 to compare moves).

  Bar chart of Avg Return % with conditional colors to highlight standouts.

5) Final polish

  Make numbers consistent (decimals, % signs), tidy legends and line thickness.

  Add a “Reset” bookmark to clear slicers.

  Quick QA pass: do cards, tables, and charts match the data?
 
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

---

### 🗂️ Artifacts (Week 4: current week)


---

🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

