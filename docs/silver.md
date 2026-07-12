# Silver Layer

## Overview

The Silver layer improves the quality and consistency of the Bronze data. This layer is responsible for validating, cleaning, and enriching the datasets while preserving their business meaning.

No aggregations are performed in this layer because aggregation represents business logic rather than data quality.

---

## Objectives

- Improve data quality
- Standardize data
- Validate records
- Detect anomalies
- Preserve analytical flexibility

---

## Table Transformations

### Orders

- Flagged delivery anomalies
- Added `is_anomaly` indicator

---

### Products

- Replaced missing product categories with **Unknown**
- Joined category translation table
- Converted Portuguese category names into English

---

### Customers

No transformation required.

Data quality checks confirmed:

- No duplicate records
- No missing primary keys

---

### Sellers

No transformation required.

Verified for:

- Null values
- Duplicate records

---

### Payments

Payment records were intentionally preserved at payment-level granularity.

Multiple payment records per order represent legitimate business behaviour rather than duplicate data.

---

### Reviews

The original CSV contained multiline review comments.

The Bronze ingestion process was modified to correctly parse multiline records.

No additional transformations were required after successful ingestion.

---

### Geolocation

Duplicate postal code prefixes were intentionally preserved.

Multiple latitude and longitude values legitimately exist for the same postal code because they represent different physical locations within the same geographical area.

---

## Characteristics

- Data Cleaning
- Data Validation
- Data Enrichment
- Schema Standardization
- No Aggregation

---

## Output

Trusted datasets ready for dimensional modelling in the Gold layer.