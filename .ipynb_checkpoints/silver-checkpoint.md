# Silver Layer

## Purpose

The Silver layer improves data quality through cleaning, validation and standardization while preserving business meaning.

## Transformations

### Orders

- Delivery anomalies flagged
- Added is_anomaly column

### Products

- Missing categories replaced with "Unknown"
- Portuguese category names translated to English

### Customers

- No transformation required

### Sellers

- No transformation required

### Order Payments

- Preserved multiple payment records
- No aggregation performed

### Order Reviews

- Fixed malformed multiline CSV parsing during Bronze ingestion
- No further transformation required

### Geolocation

- Duplicate postal code prefixes intentionally preserved because multiple latitude/longitude values legitimately belong to the same area.

## Characteristics

- Data cleaning
- Data validation
- Data enrichment
- No aggregation