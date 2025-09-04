# Phase 1 Architecture (Market Data Core)

```mermaid
flowchart LR
  RAW[raw/AAPL_daily.csv] --> ETL[etl/ingest_ohlcv.py]
  ETL --> LAKE[(lake/ohlcv as Parquet)]
  LAKE --> CLEAN[models/ cleaning & alignment]
  CLEAN --> BI[Power BI Dashboard]
```
