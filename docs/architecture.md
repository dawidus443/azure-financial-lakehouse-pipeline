┌───────────────────────────────────────────────────────────────────────────┐
│                         AZURE FINANCIAL LAKEHOUSE                         │
└───────────────────────────────────────────────────────────────────────────┘

┌────────────────────┐        ┌────────────────────────┐
│ Market Data API(s) │──────▶ │ Azure Data Factory     │
│ - stocks           │ ingest │ - Pipelines            │
│ - metadata         │        │ - Triggers (schedule)  │
└────────────────────┘        └─────────────┬──────────┘
                                            │
                                            ▼
                          ┌──────────────────────────────────────┐
                          │  Azure Data Lake Storage Gen2        │
                          │  (Hierarchical Lakehouse Layers)     │
                          │                                      │
                          │  RAW     →   BRONZE  →  SILVER → GOLD│
                          │  (raw)      (ingest)   (clean) (curated)
                          └──────────┬───────────────┬──────────┘
                                     │               │
                                     ▼               ▼
                        ┌──────────────────┐   ┌──────────────────────┐
                        │ Azure Databricks │   │ Downstream Consumers │
                        │ - Spark ETL      │   │ - Dashboards (future)│
                        │ - Delta Lakes    │   │ - ML/Apps (optional) │
                        └──────────────────┘   └──────────────────────┘

                                         ▲
                                         │
                         ┌──────────────────────────────────────┐
                         │ Azure Monitor / Log Analytics        │
                         │ - pipeline failures                  │
                         │ - data quality alerts (future)       │
                         └──────────────────────────────────────┘
