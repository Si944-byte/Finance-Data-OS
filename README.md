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

![Flowchart](https://github.com/user-attachments/assets/9b7a24d8-e616-46a8-937c-0190c9efb4ed)

---

📂 Project Layout

![Project layout](https://github.com/user-attachments/assets/05c9f00b-b75e-4d76-99a0-990fe388828f)

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

📅 Roadmap

![roadmap](https://github.com/user-attachments/assets/87fd6d22-4737-4d7f-bb6a-16f93dfa9187)

---

🖼️ Example Output

![Screenshot 2025-08-28 194355](https://github.com/user-attachments/assets/99ec77f1-4f78-4d5a-9c43-0d968fe5a17e)

---
## 🚢 Week 2 – Multi-Ticker Ingest & Finance Chart

This week’s artifact expands the Finance Data OS pipeline to handle **multiple tickers (AAPL, MSFT, TSLA)** and deliver a professional-grade visualization.

### ✅ What’s New
- **Multi-ticker ingest** with partitioned Parquet output  
- **Pandera schema validation** applied at the data lake layer  
- **Feature engineering**: 10-day Simple Moving Average (SMA10)  
- **Power BI dashboard** with:
  - Closing Price vs 10-day SMA lines  
  - Volume bars on secondary axis  
  - Dynamic chart title linked to ticker slicer  
  - Clean, finance-style formatting (line labels, neutral bars, USD + M units)  

### 📊 Example Output

![TSLA](https://github.com/user-attachments/assets/7425391e-47fc-4b47-acfe-91a0d8a9c100)

### 🗂️ Artifacts

- `Finance_Data_OS_Week2.pbix` → Power BI dashboard file (in repo files)

---



🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

