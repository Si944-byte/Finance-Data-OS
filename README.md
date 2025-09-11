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

    Overview/Compare — normalized close (start=1.0), summary table (Avg Return %, Vol, Cumulative Return %, Latest Close, CAGR %, Positive Day %), bar chart with conditional formatting.

  - DAX measures: Avg Return %, Vol (stdev of return1), Positive Day %, Latest Close, Latest SMA10, Close vs SMA10 %, Cumulative Return %, CAGR %.

  - Date table (DAX) and relationship to fact tables for robust time slicing.

  - Notebook + build log: Week 3 .ipynb and documentation added for reproducibility.

  (Week 4: optional signal prototypes—e.g., SMA crossovers with walk-forward tests—and scheduled refresh/CI.) (in progress)

---

⚡ Quick Start (Follow along with me!)

1. Clone the repo:

![Quick start](https://github.com/user-attachments/assets/9c55d018-1f03-4d41-94c7-22eef2cbe481)

2. Set up virtual environment:

![virtual environment](https://github.com/user-attachments/assets/6e670fa6-0e35-4667-8baf-138b5d87363d)

3. Install Dependencies:

![dependencies](https://github.com/user-attachments/assets/6fb5db89-88ed-459d-a833-ef7797e57a54)

4. Run the notebook:

![Jupyter notebook](https://github.com/user-attachments/assets/8ffd40a2-ec9d-4452-ac9a-efad5450b042)


---

📝 Build Logs

Build Log – Week 1
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk1

Build Log – Week 2
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk2

Build Log - Week 3
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk3

---

📈 Week 3 – Expanding History & Shipping the Feature Mart

This week’s artifact scales the Finance Data OS pipeline to 5+ years of history for multiple tickers (AAPL, MSFT, NVDA, TSLA), hardens the data lake with validation + a repair pass, and ships a tidy feature mart that powers a 3-page Power BI dashboard.

✅ What’s New

  - Long-horizon ingest (2019–2025) via yfinance(auto_adjust=True)
    Close is already adjusted — no Adj_Close needed.

  - Partitioned Parquet lake
    lake/ohlcv/ticker=<T>/year=<YYYY>/<T>_<YYYY>.parquet

  - Idempotent repair pass
    Normalize/rename, coerce types, fill ticker, and trim rows to the folder’s ticker/year.

  - Lake validation
    Required columns, null checks, numeric types, duplicate (ticker,date), and partition consistency (file path vs. row values).

  - Feature engineering v2 (saved as a single table)

    return1 — daily % return
    sma10 — 10-day simple moving average
    vol20 — 20-day rolling stdev of close

  - Feature Mart shipped → lake/feature_mart.parquet
    (columns: date, ticker, close, return1, sma10, vol20)

  - Power BI dashboard (3 pages)

    1. Price vs SMA10 – KPI cards (Latest Close, Latest SMA10, Close vs SMA10 %), line chart of Close vs SMA10

    2. Volatility & Distribution – Daily return line, vol20 trend with reference lines, histogram of daily returns

    3. Overview / Compare – Normalized Close (start = 1.0), summary table (Avg Return %, Vol, Cumulative Return %, Latest Close, CAGR %, Positive Day %), bar chart with conditional formatting to highlight leaders

  - DAX measures & Date table
    Avg Return %, Vol (stdev of return1), Positive Day %, Latest Close, Latest SMA10, Close vs SMA10 %, Cumulative Return %, CAGR %, plus a proper Date table for robust time slicing.

  - Design polish
    Finance-style cards, consistent axes/units, subtle reference lines, and rule-based highlighting for outliers.
 
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
- Small design polish matters: Finance-style cards, subtle gridlines, neutral palette, and consistent units (%, USD) improve perceived quality without extra complexity.

---

### 🗂️ Artifacts (Week 3: current week)

Week 3 Power BI Dashboards:



Exploratory Analysis (Charts) (Then used in PowerBI as part of dashboard)
Using matplotlib, created quick visualizations for sanity check:

1. **Normalized Close (AAPL, MSFT, TSLA, NVDA)**  
   - Highlights NVDA outperformance relative to peers.
     
![Normalized Close](https://github.com/user-attachments/assets/493a5365-309e-47ae-b74a-1363b1fba640)

2. **Distribution of Daily Returns (AAPL)**  
   - Bell-curve centered at 0, fat tails present.
  
![Daily returns](https://github.com/user-attachments/assets/a33598d7-2910-4106-a776-dc206a56b322)

3. **Rolling Volatility (20-day, AAPL)**  
   - Volatility clustering clearly visible.
  
![Rolling Volatility ](https://github.com/user-attachments/assets/d459e237-15c2-41fa-ad89-406df4be91d1)

4. **Daily Return Time Series (AAPL)**  
   - Sharp spikes during market stress periods.

![Daily Return ](https://github.com/user-attachments/assets/13ec96af-a88d-4030-8c94-9c294346c04e)

5. **Close vs SMA10 (AAPL)**  
   - SMA smooths short-term fluctuations, trend captured well.
  
![Close vs SMA10](https://github.com/user-attachments/assets/5a0c6caa-8f97-41b5-b977-8839fb8ed218)

---

🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

