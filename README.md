# E-Commerce Data Warehouse using PySpark

## Project Overview

This project implements an end-to-end Data Warehouse for the Olist Brazilian E-commerce dataset using the Medallion Architecture (Bronze → Silver → Gold). The pipeline ingests raw transactional data, validates and cleans it using PySpark, and transforms it into an analytics-ready Star Schema.

The project demonstrates modern Data Engineering concepts including:

- Data ingestion
- Data profiling
- Data quality validation
- Data cleaning and standardization
- Dimensional modeling
- Star schema design
- Business analytics using SQL

---

## Objectives

The primary objective of this project is to simulate a real-world Data Engineering workflow by building an analytical data warehouse from raw transactional data.

The project focuses on:

- Preserving raw data integrity
- Improving data quality through validation and standardization
- Designing an efficient dimensional model
- Supporting analytical SQL queries for business intelligence

---

## Dataset

The project uses the **Olist Brazilian E-Commerce Dataset**.

Source tables include:

- Customers
- Orders
- Order Items
- Products
- Sellers
- Payments
- Reviews
- Geolocation
- Product Category Translation

---

## Technology Stack

| Technology | Purpose |
|------------|----------|
| Python | Programming Language |
| PySpark | Distributed Data Processing |
| SQL | Business Analytics |
| Parquet | Columnar Storage |
| Jupyter Notebook | Development Environment |
| Git | Version Control |

---

## Architecture

*(Insert Architecture Diagram Here)*

---

## Medallion Architecture

The warehouse follows the Medallion Architecture.

```
Raw CSV
    ↓
 Bronze
    ↓
 Silver
    ↓
 Gold
    ↓
 SQL Analytics
```

Documentation

- Bronze Layer → docs/bronze.md
- Silver Layer → docs/silver.md
- Gold Layer → docs/gold.md

---

## Key Features

- End-to-End ETL/ELT Pipeline
- Bronze, Silver and Gold Layers
- Data Profiling
- Data Validation
- Data Standardization
- Star Schema
- Business-Oriented SQL Analytics

---

## Project Structure

```text
project/

├── data/
├── bronze/
├── silver/
├── gold/

├── notebooks/
│   ├── 01_bronze_layer.ipynb
│   ├── 02_silver_layer.ipynb
│   ├── 03_gold_layer.ipynb
│   └── 04_sql_analytics.ipynb

├── docs/
│   ├── bronze.md
│   ├── silver.md
│   └── gold.md

├── diagrams/

└── README.md
```

---

## Future Improvements

- Incremental Data Loading
- Schema Evolution
- Delta Lake
- Apache Airflow
- Cloud Deployment
- Power BI Dashboard
