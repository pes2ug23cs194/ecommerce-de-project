# Gold Layer

## Purpose

The Gold layer organizes cleaned data into a Star Schema optimized for analytical queries.

## Fact Table

### fact_order_items

Grain:

One row represents one product purchased within an order.

### Foreign Keys

- customer_id
- product_id
- seller_id

### Metrics

- price
- freight_value
- delivery_days

### Order Attributes

- order_status
- is_late
- is_anomaly
- order_purchase_timestamp

---

## Dimension Tables

### dim_customers

- customer_id
- customer_unique_id
- customer_city
- customer_state

### dim_products

- product_id
- product_category_name_en
- product_weight_g
- product_length_cm
- product_height_cm
- product_width_cm
- product_photos_qty

### dim_sellers

- seller_id
- seller_city
- seller_state

---

## Design Decisions

- Star Schema adopted for analytical workloads.
- Item-level grain chosen to preserve detailed transactional data.
- Aggregations intentionally left for analytical SQL queries.