# Massive.com AAPL Stock Pipeline & Power BI Dashboard

End-to-end Microsoft Fabric project to **automatically ingest, process, and visualize** daily AAPL stock bars from the Massive.com API.

![Dashboard](AAPLStockDashboard.png)

## Features
- **Fully automated daily pipeline**: Scheduled ingestion of 30-day batches from Massive.com API
- Growing historical Delta table with deduplication on Date
- PySpark notebooks for flattening nested JSON and cleaning data
- Interactive Power BI dashboard with candlestick trends, latest price, daily % change, volume analysis, and date slicers

## Automation
The entire workflow runs **hands-free on a daily schedule** in Microsoft Fabric:

- **Daily Trigger**: Recurring schedule starts the pipeline automatically every day.
- **Ingestion**: Copy data activity fetches the latest 30-day JSON batch from Massive.com API and writes raw file to lakehouse Files.
- **Processing**:
  - Notebook 1 (Flatten Stock JSON): Explodes nested "results" array into daily rows, casts types, derives Date, saves flattened table.
  - Notebook 2 (MassiveCleanUp): Loads flattened table, renames columns, deduplicates on Date, and **appends** new unique rows to final growing table (`aapl_daily_massive`).
- **Growth & Dedup**: Append mode + full-table dedup ensures clean, accumulating history over time (new trading days added daily).
- **Dashboard**: Power BI report connects live to the lakehouse table and refreshes with new data.

## Screenshots
| Dashboard Overview | Table Preview | Pipeline Canvas |
|--------------------|---------------|-----------------|
| ![Dashboard](AAPLStockDashboard.png) | ![Table Preview](TablePreview.png) | ![Pipeline](Pipeline.png) |

## Files
- `MassiveReport1.pbix` – Power BI report file
- `MassiveReport1.pdf` – Exported dashboard PDF

## Tools Used
- **Microsoft Fabric** (trial): Pipeline (scheduled), Lakehouse (storage), Notebooks (PySpark)
- **Power BI** (web): Candlestick chart, line chart, bar chart, KPI cards, date slicer

Portfolio project by Sean Dunleavy  
GitHub: https://github.com/seandunleavy/Massive-Stock-Pipeline-PowerBI
