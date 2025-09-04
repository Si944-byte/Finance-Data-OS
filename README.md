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

https://github.com/Si944-byte/Finance-Data-OS/blob/main/docs/img/Untitled%20diagram%20_%20Mermaid%20Chart-2025-09-04-222054.png

---

📂 Project Layout

docs/       # architecture diagrams, notes

artifacts/  # Power BI files, exported charts

Build Logs/ # Weekly build logs

notebooks/  # Jupyter notebooks (Week 1, Week 2, …)

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

Week 3 – Expanding History & Feature Store (🚧 in progress)

  - Ingest 5 years of daily data per ticker

  - Extend feature engineering

  - Ship Feature Mart v2

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

### 🗂️ Artifacts

Finance_Data_OS_Week2.pbix
 → Power BI dashboard

https://github.com/Si944-byte/Finance-Data-OS/blob/main/artifacts/week2/Finance-Data-OS-Week%202.pbix

- Example output charts are shown in artifacts/week2/:
  
 https://github.com/Si944-byte/Finance-Data-OS/tree/main/artifacts/week2 

 <img width="885" height="551" alt="image" src="https://github.com/user-attachments/assets/47934f98-3fb1-4bde-9e2d-79c4640da7bd" />

---

🤝 Contributing

This is an open project for learning and sharing best practices in data engineering for financial markets.
Suggestions, issues, and PRs are welcome.

---

📜 License

MIT License — see LICENSE for details.

