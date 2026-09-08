# Olist E-Commerce Data Warehouse & Business Analytics

## Project Overview

This project implements an end-to-end Data Warehouse and Business Analytics
workflow for the Olist Brazilian E-Commerce dataset using the Medallion
Architecture (Bronze → Silver → Gold).

The pipeline ingests raw transactional data, validates and cleans it using
PySpark, and transforms it into an analytics-ready Star Schema. The resulting
Gold layer is then used for business-oriented analysis of customer behavior,
seller performance, and customer retention.

The project demonstrates modern Data Engineering and Business Analytics
concepts including:

- Data ingestion
- Data profiling
- Data quality validation
- Data cleaning and standardization
- Dimensional modeling
- Star schema design
- Analytical SQL
- Customer segmentation
- Seller performance analysis
- Cohort retention analysis
- Business dashboarding
- Data-driven business recommendations

---

## Objectives

The primary objective of this project is to simulate a real-world Data
Engineering and Business Analytics workflow by building an analytical data
warehouse from raw transactional data and using the resulting data to answer
business questions.

The project focuses on:

- Preserving raw data integrity
- Improving data quality through validation and standardization
- Designing an efficient dimensional model
- Building analytics-ready datasets
- Supporting analytical SQL queries for business intelligence
- Identifying customer retention opportunities
- Evaluating seller operational performance
- Translating analytical findings into business recommendations

---

## Dataset

The project uses the **Olist Brazilian E-Commerce Dataset**.

The dataset contains approximately 100K orders across 9 relational datasets.

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
|------------|---------|
| Python | Data analysis and transformation |
| PySpark | Distributed data processing and ETL |
| Pandas | Customer and cohort analysis |
| Spark SQL | Analytical queries |
| SQL | Business analytics |
| PostgreSQL | Relational database |
| Parquet | Columnar storage |
| Excel | Business dashboard |
| Jupyter Notebook | Development and analysis |
| Git | Version control |

---

## Architecture

The project follows a layered data architecture that separates data
ingestion, transformation, modeling, and business analysis.

![Architecture](diagrams/architecture.png)

---

## Medallion Architecture

The warehouse follows the Medallion Architecture.

```text
Raw CSV
   ↓
Bronze
   ↓
Silver
   ↓
Gold
   ↓
Business Analytics
   ↓
Excel Dashboard
