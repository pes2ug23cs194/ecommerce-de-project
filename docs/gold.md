# Gold Layer

## Overview

The Gold layer contains analytics-ready datasets organised using a Star Schema.

This layer is optimized for reporting, dashboarding, and business intelligence workloads.

---

## Objectives

- Build a dimensional model
- Support analytical SQL queries
- Reduce query complexity
- Improve reporting performance

---

# Star Schema

*(Insert Star Schema Diagram Here)*

---

## Fact Table

### fact_order_items

**Grain**

One row represents one product purchased within an order.

---

### Foreign Keys

- customer_id
- product_id
- seller_id

---

### Metrics

- price
- freight_value
- delivery_days

---

### Order Attributes

- order_status
- is_late
- is_anomaly
- order_purchase_timestamp

---

## Dimension Tables

### dim_customers

Contains descriptive customer information.

Columns

- customer_id
- customer_unique_id
- customer_city
- customer_state

---

### dim_products

Contains descriptive product information.

Columns

- product_id
- product_category_name_en
- product_weight_g
- product_length_cm
- product_height_cm
- product_width_cm
- product_photos_qty

---

### dim_sellers

Contains seller information.

Columns

- seller_id
- seller_city
- seller_state

---

## Design Decisions

### Why fact_order_items instead of fact_orders?

The warehouse was modeled at the order-item grain to preserve the most detailed level of information.

This enables analysts to perform both product-level and order-level analysis through aggregation.

Aggregating to an order-level fact table would permanently lose product-level detail.

---

### Why were aggregations not stored?

Aggregations are business-specific and are therefore generated during SQL analytics rather than being permanently stored in the warehouse.

---

## Output

The Gold layer serves as the analytical foundation for SQL queries, dashboards, and business intelligence applications.