# E-commerce Customer Segmentation & Conversion Funnel Analysis

End-to-end data pipeline on Databricks that processes 42M raw clickstream events into a lakehouse, segments customers by RFM scoring, and surfaces actionable business recommendations.

**Stack:** PySpark · Delta Lake · Databricks Free Edition · Databricks SQL · matplotlib

---

## What this project does

Raw e-commerce event logs (view / cart / purchase) are ingested and transformed through a Bronze→Silver→Gold medallion architecture. The Gold layer feeds two outputs:

- **Conversion funnel** — session-level drop-off rates by product category
- **Customer segmentation** — RFM-scored segments with revenue and recency profiles

Key findings from October 2019 data:
- Champions (5.7% of buyers) account for 32% of total revenue ($73.7M)
- 9,345 At-Risk customers represent $15.4M in recoverable revenue
- Electronics is the largest funnel leak: 55K abandoned cart sessions at a 13.5% abandonment rate

---

## Repository structure

```
├── E-commerce Customer Segmentation Analysis.ipynb   # main notebook (run top to bottom)
└── README.md
```

---

## Pipeline overview

| Layer | Table | Description |
|---|---|---|
| Bronze | `bronze_events` | Raw CSV ingested as strings, no transformations |
| Silver | `silver_events` | Typed, deduplicated, null/invalid rows removed |
| Gold | `gold_funnel_daily` | Session-level conversion funnel by category and date |
| Gold | `gold_rfm_customers` | Per-customer RFM scores and segment labels |
| Gold | `gold_segment_summary` | Segment-level revenue, spend, and recency aggregates |

---

## Dataset

REES46 [eCommerce behavior data from multi category store](https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store) — October 2019, ~42M events, 5.6 GB. Downloaded automatically via `kagglehub` on first run.
