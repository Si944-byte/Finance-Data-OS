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

![Project layout](https://github.com/user-attachments/assets/2691b0fb-c9b9-459b-bf33-da1abed1068e)

---

⚡ Quick Start (Follow along with me!)

1. Clone the repo:

![Quick start](https://github.com/user-attachments/assets/8b24e3aa-068f-4593-b686-18a2f211aa1c)

2. Set up virtual environment:

![virtual environment](https://github.com/user-attachments/assets/95db276c-beb6-4d2b-8c8d-b4ed2e97638d)

3. Install Dependencies:

![dependencies](https://github.com/user-attachments/assets/e0d7ee6f-f569-47d3-b2a3-0a29af006dbd)

4. Run the notebook:

![Jupyter notebook](https://github.com/user-attachments/assets/ec927724-718d-41d2-91fc-b6e48124e0f2)

---

📅 Roadmap

![roadmap](https://github.com/user-attachments/assets/a7ece15d-08a0-4eab-b8c1-d1b205c003dc)


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

