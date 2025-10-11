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

Week 2 – Multi-Ticker Ingest & Finance Chart ✅

Week 3 – Expanding History & Feature Store ✅

Week 4 – Signals, Backtest & 3-Page Power BI ✅

Week 5 – Costs, Controls & Tuning ✅  

Week 6 - Rolling Metrics, Cost Modeling and Cleaner Pipeline ✅

Week 7 - Ship a reliable, incremental workflow for signals/backtests/trades/tuning with clear manifests, parity validation, and a Power BI page for tuning results.✅

Scope (what’s in)

fdos CLI with subcommands: signals, backtest, trades, tune

Incremental runs via --since with append-only writes and (ticker, date) de-dupe

Per-dataset *.manifest.json (row counts, timestamps, config hash)

Parity check (v7 vs v6) on NVDA/TSLA (CAGR, Sharpe, MaxDD)

Power BI page: Tuning Results (heatmap + top configs + optional scatter)

CLI v0.7.0 (fdos) with shared options --config --since --verbose

Lake outputs

lake/backtest_daily_v3.parquet (+ .manifest.json)

lake/trades_v3.parquet (+ .manifest.json)

lake/tuning_mart.parquet (+ .manifest.json)

Parity script: scripts/compare_parity_nopandas.py

Run logs: ./runs/<run_id>/run.log

Power BI: “Tuning Results” page added to PBIX

Docs: “About this report (Week-7)” section

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

Build Log - Week 6
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk6

Build Log - Week 7
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk7

---

🗺️ Week 7 — What's New

CLI v0.7.0 with Typer: fdos run signals | backtest | trades | tune

Incremental runs: --since appends only new (ticker, date) rows; idempotent by design

Run logging: per-run folder ./runs/<run_id>/run.log with INFO to console, DEBUG to file

Manifests everywhere: sibling *.manifest.json (row counts, appended_rows, hashes, UTC ts) for backtest, trades, tuning

UTC fix: timezone-aware ISO-8601 timestamps (no more utcnow() deprecation)

Parity gate v7 vs v6 (NVDA/TSLA): thresholds |ΔCAGR| < 0.5pp, |ΔSharpe| < 0.05, |ΔMaxDD| < 0.5pp

Parity script (no-pandas option) to avoid Windows/NumPy wheel issues

Power BI “Tuning Results” page:

    - Heatmap (Sharpe by slow×fast), detail table, bubble (MaxDD vs Sharpe, size=Days)

    - Slicers: ticker, vol_window, vol_threshold_pct, cost_bps

Pytest hygiene: pytest.ini now ignores notebooks/src; CLI tests green

Docs: new “About this report (Week-7)” + quickstart commands

---

### 🧠 What I Learned

**Week 7 – Push-button backtest, parameter sweeps and one-command workflows**  

- Small, reliable increments beat full refreshes. --since + manifests made rebuilds faster and explanations easier.

- Manifests are the truth. existing_rows / appended_rows / final_rows became our quickest health check and parity aid.

- Windows packaging can bite. Pandas/NumPy wheels and pandas._libs errors happen; having a pandas-free fallback parity script unblocked release.

- Always use timezone-aware timestamps. Swapping to datetime.now(timezone.utc) fixed deprecation noise and improved auditability.

- Tests need scoping. A tight pytest.ini (ignore notebooks, pick tests/) prevented accidental imports and sped up feedback.

- Power BI benefits from minimalism. Fewer visuals + clear KPI cards + consistent number formats make the Tuning page usable even with a small grid.

- De-dupe keys matter. Appending on (ticker, date) with schema checks avoided silent duplication when re-running stages.

- Logging levels pay off. INFO for users, DEBUG to file gave us readable consoles and deep diagnostics when we needed them.

- A tiny sweep is fine for plumbing. Proved the end-to-end path (CLI → parquet → manifest → PBIX) before expanding the parameter grid.
  
---

### 🗂️ Artifacts (Week 7: current week)

Week 7 - Notebook
https://github.com/Si944-byte/Finance-Data-OS/blob/main/notebooks/Week_7_Walkthrough

Dashboard Pages:

Page 1 - Signals 
![Screenshot 2025-10-10 163249](https://github.com/user-attachments/assets/c55575b3-2426-4515-9315-4b44e530b91b)

Page 2 - Back-test
![Screenshot 2025-10-10 163411](https://github.com/user-attachments/assets/6bf09593-5574-48e9-a919-5a92af75c5de)

Page 3 - Tuning Results
![Screenshot 2025-10-10 172348](https://github.com/user-attachments/assets/0cbdcce3-1176-4647-8ec2-dc4f62ebf5d9)

Page 4 - Summary Page
![Screenshot 2025-10-10 163644](https://github.com/user-attachments/assets/8c5070c5-aef8-4153-8586-46de508dcb94)

Page 5 - About Page
![Screenshot 2025-10-10 195946](https://github.com/user-attachments/assets/bc3f640b-efe8-4e91-9cf6-9bca3383407d)

---

🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

