# Finance Data OS

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Python](https://img.shields.io/badge/python-3.11+-blue.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)

> **An end-to-end big data system for financial markets**: ingest raw market data, store efficiently in Parquet, validate with Pandera, engineer features, and visualize in Power BI dashboards.

---

## 🚀 Project Goal
To build a **modular financial data platform** that takes raw equities, options, and macroeconomic datasets and transforms them into analytics-ready features for trading and investment research.

---

## 🏗️ Architecture (Phase 1)

    flowchart LR
      RAW[raw/*.csv (starter: AAPL_daily.csv)] --> ETL[etl/ingest_ohlcv.py]
      ETL --> LAKE[(lake/ohlcv as Parquet)]
      LAKE --> VALIDATE[Pandera Schema Validation]
      VALIDATE --> FEATURES[Feature Engineering]
      FEATURES --> MART[(mart/ohlcv_features.parquet)]
      MART --> BI[Power BI Dashboard]

---

📂 Project Layout

etl/        # ingestion scripts (CSV/API → Parquet)

models/     # transforms & features

docs/       # architecture diagrams, notes

tests/      # schema/data tests

lake/       # raw parquet data lake

mart/       # analytics-ready outputs

raw/        # input CSVs for testing

---

⚡ Quick Start (Follow along with me!)

1. Clone the repo:

    git clone https://github.com/SI944-byte/finance-data-os.git
    cd finance-data-os

2. Set up environment:

    python -m venv .venv

    # Windows
    .venv\Scripts\activate.bat

    # Mac/Linux
    source .venv/bin/activate

3. Install Dependencies:

    pip install -r requirements.txt

4. Run the notebook:

    jupyter notebook Finance_Data_OS_Week1_Notebook.ipynb

---

📅 Roadmap

  Ingest OHLCV → Parquet (complete)
  
  Schema validation with Pandera (complete)
  
  Power BI dashboard (prototype) (complete)
  
  Add macroeconomic data
  
  Feature store v1
  
  Options Greeks & Risk Cockpit
  
  Signal research & backtesting
  
  API + lightweight UI

  ---

🖼️ Example Output
![Screenshot 2025-08-28 194355](https://github.com/user-attachments/assets/99ec77f1-4f78-4d5a-9c43-0d968fe5a17e)

---

🤝 Contributing
This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License
MIT License — see LICENSE for details.

