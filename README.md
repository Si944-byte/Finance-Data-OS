# Finance Data OS

[![CI](https://github.com/SI944-byte/finance-data-os/actions/workflows/ci.yml/badge.svg)](https://github.com/SI944-byte/finance-data-os/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Python](https://img.shields.io/badge/python-3.11+-blue.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)

> **An end-to-end big data system for financial markets**: ingest raw market data, store efficiently in Parquet, validate with Pandera, engineer features, and visualize in Power BI dashboards.

---

## 🚀 Project Goal
To build a **modular financial data platform** that takes raw equities, options, and macroeconomic datasets and transforms them into analytics-ready features for trading and investment research.

---

## 🏗️ Architecture (Phase 1)
```mermaid
flowchart LR
  RAW[raw/AAPL_daily.csv] --> ETL[etl/ingest_ohlcv.py]
  ETL --> LAKE[(lake/ohlcv as Parquet)]
  LAKE --> VALIDATE[Pandera Schema Validation]
  VALIDATE --> FEATURES[Feature Engineering]
  FEATURES --> MART[(mart/ohlcv_features.parquet)]
  MART --> BI[Power BI Dashboard]
📂 Project Layout
graphql
Copy code
etl/        # ingestion scripts (CSV/API -> Parquet)
models/     # transforms & features
docs/       # architecture & data contracts
tests/      # schema/data tests
lake/       # Parquet "data lake"
mart/       # analytics-ready outputs
raw/        # input CSVs for testing
⚡ Quick Start
Clone the repo:

bash
Copy code
git clone https://github.com/SI944-byte/finance-data-os.git
cd finance-data-os
Set up environment:

bash
Copy code
python -m venv .venv
# Mac/Linux
source .venv/bin/activate
# Windows (PowerShell)
.venv\Scripts\Activate.ps1

pip install -r requirements.txt
Run the notebook:

bash
Copy code
jupyter notebook Finance_Data_OS_Week1_Notebook.ipynb
📅 Roadmap
 Ingest OHLCV → Parquet

 Schema validation with Pandera

 Power BI dashboard (prototype)

 Add macroeconomic data

 Feature store v1

 Options Greeks & Risk Cockpit

 Signal research & backtesting

 API + lightweight UI

📖 Docs
Architecture (Phase 1)

Feature Store Contract

🖼️ Example Output
(Matplotlib quick chart from notebook)

🤝 Contributing
This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

📜 License
MIT License — see LICENSE for details.

