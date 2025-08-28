# Finance Data OS

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



[![CI](https://github.com/SI944-byte/finance-data-os/actions/workflows/ci.yml/badge.svg)](https://github.com/SI944-byte/finance-data-os/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Python](https://img.shields.io/badge/python-3.11+-blue.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)

