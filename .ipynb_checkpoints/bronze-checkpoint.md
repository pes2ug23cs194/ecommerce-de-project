# Bronze Layer

## Purpose

The Bronze layer stores raw source data exactly as received from the Olist dataset.

## Input

CSV Files

- Customers
- Orders
- Order Items
- Products
- Sellers
- Payments
- Reviews
- Geolocation
- Category Translation

## Processing

- Read CSV files
- Infer schema
- Convert to Parquet
- Store without modification

## Characteristics

- No transformations
- No cleaning
- No aggregation
- Preserves original data
- Supports data recovery and auditing