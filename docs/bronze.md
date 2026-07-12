# Bronze Layer

## Overview

The Bronze layer represents the raw ingestion layer of the data warehouse. Its responsibility is to preserve source data exactly as received from the operational system without applying business logic or transformations.

This layer acts as the single source of truth and allows the pipeline to be reprocessed whenever downstream logic changes.

---

## Objectives

- Preserve original source data
- Create an immutable raw data layer
- Enable pipeline reproducibility
- Support auditing and recovery

---

## Input

Raw CSV files

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

## Processing Steps

1. Read CSV files using PySpark.
2. Infer data schema.
3. Store datasets in Parquet format.
4. Preserve original records without modification.

---

## Design Decisions

### Why no transformations?

Business rules evolve over time.

Keeping the Bronze layer untouched allows the Silver layer to be rebuilt without requiring access to the original source system.

### Why Parquet?

Parquet is a columnar storage format that provides:

- Better compression
- Faster analytical queries
- Reduced storage consumption
- Predicate pushdown

---

## Output

All source datasets stored as raw Parquet files.

No cleaning.

No filtering.

No aggregation.

No enrichment.