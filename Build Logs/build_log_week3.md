# 🛠 Build Log — Week 3

## Week Overview
The focus this week was on **validating the data lake, repairing schema issues, and building the feature mart** with engineered factors for downstream analytics. We also created exploratory charts (Python/matplotlib) and prepared the data for Power BI dashboards.

---

## 🔹 Day 1 — Setup & Lake Repair
- Activated virtual environment and confirmed dependencies with `requirements.txt`.  
- Verified parquet lake files pulled in Week 2.  
- Noticed schema mismatches (`Adj_Close` missing, column naming inconsistent).  
- Added a **repair step** to standardize columns → enforced:  
  - `date`, `ticker`, `open`, `high`, `low`, `close`, `volume`.  
- Re-saved repaired parquet partitions per ticker/year.  

✅ Outcome: lake directory consistent, all partitions aligned.

---

## 🔹 Day 2 — Validation Framework
- Wrote validation checks for:  
  - Required columns present  
  - Null handling  
  - Numeric data types  
  - Duplicate `(ticker, date)` keys  
  - Partition consistency (ticker/year vs file path)  
- Iterated after multiple assertion errors → refined coercion for datetime and numeric types.  
- Final validation: **28 files passed** ✅  

---

## 🔹 Day 3 — Feature Mart Build
- Engineered new features:
  - `return1`: daily % return  
  - `sma10`: 10-day simple moving average  
  - `vol20`: 20-day rolling volatility  
- Added safeguards:
  - Alignment checks between features and base dataframe  
  - Dropped null rows post-feature engineering  
  - Prevented duplicate ticker/date combinations  
- Saved mart to `lake/feature_mart.parquet`.  

✅ Mart complete with ~6,000 rows across 4 tickers (2019–2025).

---

## 🔹 Day 4 — Exploratory Analysis (Charts)
Using matplotlib, created quick visualizations for sanity check:

1. **Normalized Close (AAPL, MSFT, TSLA, NVDA)**  
   - Highlights NVDA outperformance relative to peers.  

2. **Distribution of Daily Returns (AAPL)**  
   - Bell-curve centered at 0, fat tails present.  

3. **Rolling Volatility (20-day, AAPL)**  
   - Volatility clustering clearly visible.  

4. **Daily Return Time Series (AAPL)**  
   - Sharp spikes during market stress periods.  

5. **Close vs SMA10 (AAPL)**  
   - SMA smooths short-term fluctuations, trend captured well.  

✅ All charts exported as `.png` for README inclusion.

---

## 🔹 Day 5 — Power BI Prep
- Exported `feature_mart.csv` for easy import into Power BI.  
- Designed a **3-page dashboard** structure:  
  1. **Trend Tracking** → Close vs SMA10  
  2. **Risk/Return** → Daily returns + Rolling volatility  
  3. **Comparative View** → Normalized close across tickers  

---

## 🚀 Week 3 Deliverables
- Validated, repaired, and consistent parquet lake.  
- Feature mart with engineered signals.  
- Exploratory charts (Python/matplotlib).  
- CSV/Parquet ready for Power BI dashboards.  
- Documentation updated (README + Build Log).  

---

👉 Next Week (Week 4): Extend features (longer moving averages, Bollinger Bands, sector benchmarks), and deepen Power BI visuals with measures (Sharpe ratio, rolling averages).  
