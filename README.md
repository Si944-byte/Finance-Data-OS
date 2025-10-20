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

Week 7 - Push-button backtest, parameter sweeps and one-command workflows ✅

Week 8 - Deterministic parameter tuning + clean analytics ✅

Objectives

    - Reproducible sweeps via CLI

    - Persist results to a stable parquet dataset

    - Visualize “best combo by ticker” in Power BI

Deliverables

    - CLI: fdos.cli tune (opts above)

    - Parquet: lake/tuning_mart.parquet/tuning-*.parquet (append-safe)

    - Locked schema + tests

    - Power BI Tuning Results page (Sharpe, CAGR, MaxDD, Win-Rate; heatmap & scatter)

    - Run guide + troubleshooting

Plan (Mon–Fri)

    Mon: finalize YAML + wire CLI; log combos

    Tue: pyarrow write path; {i} basename; seed determinism

    Wed: schema/tests; --max-combos, batching, parallel mode

    Thu: build visuals/measures/slicers; refresh & validate

    Fri: polish docs; end-to-end run; release notes & publish

Success

    - Tests green; ≥1 shard & >0 rows written

    - Power BI loads with no field/aggregate errors

    - Slicers (ticker/vol/cost) drive visuals correctly

    - Same seed ⇒ same ordering

Risks → Mitigations

    - Schema drift → lock schema + tests

    - Combo explosion → --max-combos + early logging

    - Windows quoting → document ^ + provide Python one-liners

    - Arrow “schema” conflicts → build Table once; don’t double-pass schema; use {i} template

Next (Week 9)

    - Swap in real KPI engine

    - Add new parameter groups (RSI/ATR/…)

    - Incremental, date-partitioned writes

    - Stability/Sensitivity charts by period

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

Build Log - Week 8
https://github.com/Si944-byte/Finance-Data-OS/blob/main/Build%20Logs/Build%20Log%20wk8

---

🗺️ Week 8 — What's New

- Deterministic tuning CLI: fdos.cli tune with --config/--since/--max-combos/--seed/--batch-rows/--parallel-by.

- Tuning Mart (parquet): sharded writes to lake/tuning_mart.parquet/tuning-{i:06d}.parquet, stable schema.

- Power BI page – Tuning Results: cards, heatmap, risk-return scatter, and “Best” badges by ticker.

- Guardrails: combo cap, batching, seed control, and clear logging (grids -> …, combos = …).

- Tests & docs: schema lock + smoke run; quick verification & troubleshooting.

---

### 🧠 What I Learned

**Week 8 – Parameter Tuning + Analytics**  

- Determinism pays off. A single --seed made runs explainable, debuggable, and demo-ready.

- PyArrow gotchas. Passing schema via both Scanner and write_dataset causes “multiple values for schema”; convert rows to a Table with the schema, then write with a {i} basename_template for safe sharding.

- Names > everything. One mis-named key (cost_bps vs costs_bps) zeroed out combinations and silently blocked writes; strict schema + tests saved the day.

- Guardrails matter. --max-combos and --batch-rows prevented runaway sweeps and memory spikes.

- Power BI specifics.

    - Use Don’t summarize for scatter axes (e.g., Max DD %, Sharpe).

    - Measures vs columns: choose columns for the point plot and measures for cards/aggregates.

    - Heatmap (matrix) becomes useful once schema is stable and slicers are clean.

- Windows shell quirks. Multi-line commands need ^; for quick checks, a Python heredoc is faster and less brittle.

- Logging for trust. Printing grids -> … and combos=… upfront catches config mistakes early.

---

### 🗂️ Artifacts (Week 8: current week)

Dashboard Pages:

Page 1 - Signals 
![Screenshot 2025-10-10 163249](https://github.com/user-attachments/assets/c55575b3-2426-4515-9315-4b44e530b91b)

Page 2 - Back-test
![Screenshot 2025-10-10 163411](https://github.com/user-attachments/assets/6bf09593-5574-48e9-a919-5a92af75c5de)

Page 3 - Tuning Results
![Screenshot 2025-10-20 140102](https://github.com/user-attachments/assets/254177a2-c4cb-4ecb-8631-e3b88b4adb3c)

Page 4 - Summary Page
![Screenshot 2025-10-10 163644](https://github.com/user-attachments/assets/8c5070c5-aef8-4153-8586-46de508dcb94)

Page 5 - About Page
![Screenshot 2025-10-20 183211](https://github.com/user-attachments/assets/ef5bec65-22db-4872-99e3-20d487401d94)


---

🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

