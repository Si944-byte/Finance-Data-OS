# Feature Store Contract (v0)

| Column  | Type   | Description                         |
|---------|--------|-------------------------------------|
| Date    | Date   | Trading day                         |
| Ticker  | String | Symbol (e.g., AAPL)                 |
| Open    | Float  | Open price                          |
| High    | Float  | High price                          |
| Low     | Float  | Low price                           |
| Close   | Float  | Close price                         |
| Volume  | Int64  | Shares traded                       |
| Return1 | Float  | Close/Close(-1) - 1                 |
| SMA10   | Float  | 10-day simple moving average Close  |
