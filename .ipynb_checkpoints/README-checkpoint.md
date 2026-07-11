# E-Commerce Data Warehouse using PySpark

## Overview

This project implements an end-to-end data warehouse using the Medallion Architecture (Bronze → Silver → Gold) on the Olist Brazilian E-commerce dataset. The pipeline ingests raw CSV files, performs data cleaning and validation using PySpark, and builds a Star Schema for analytical workloads.

## Tech Stack

- Python
- PySpark
- SQL
- Parquet
- Jupyter Notebook
- Git

## Architecture

(Add architecture diagram here)

## Medallion Architecture

- Bronze Layer - Raw Data Storage
- Silver Layer - Data Cleaning & Validation
- Gold Layer - Star Schema & Analytics

Detailed documentation:

- [Bronze Layer](docs/bronze.md)
- [Silver Layer](docs/silver.md)
- [Gold Layer](docs/gold.md)

## Project Structure

```
project/
│
├── data/
├── bronze/
├── silver/
├── gold/
│
├── notebooks/
│   ├── 01_bronze_layer.ipynb
│   ├── 02_silver_layer.ipynb
│   ├── 03_gold_layer.ipynb
│   └── 04_sql_analytics.ipynb
│
├── docs/
│
├── diagrams/
│
└── README.md
```

## Future Improvements

- Incremental Loading
- Delta Lake
- Apache Airflow
- Power BI Dashboard
- Cloud Deployment