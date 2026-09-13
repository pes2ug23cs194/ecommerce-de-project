# Business Insights — Olist E-Commerce Gold Layer

Findings from the gold-layer analytics marts (customer segmentation, seller
risk, cohort retention), computed via Spark SQL on ~93K delivered orders.

---

## 1. Retention, not acquisition, is the constraint

97% of customers place exactly one order. Month-1 repeat purchase rate
across 20 monthly cohorts is 0.48%, and it declines to under 0.2% by month 9,
recovering only slightly by month 10–11 before dropping again at month 12.

| Months since first purchase | Retention % |
|---|---|
| 1 | 0.48% |
| 2 | 0.34% |
| 3 | 0.26% |
| 6 | 0.23% |
| 9 | 0.17% |
| 12 | 0.17% |

**Recommendation:** a post-purchase win-back flow (targeted at day 30–45)
would likely move the needle more than acquisition spend, given how few
customers return at all. See the opportunity-sizing analysis below.

## 2. Revenue concentration is real but moderate

| Segment | Customers | % of customers | Revenue (R$) | % of revenue | Avg R$/customer |
|---|---|---|---|---|---|
| Recent High-Value | 23,600 | 25.28% | 5,556,234.68 | 42.02% | 235.43 |
| Lapsed High-Value | 23,078 | 24.72% | 5,458,910.12 | 41.29% | 236.54 |
| Low-Value One-Time | 46,222 | 49.51% | 2,177,945.00 | 16.47% | 47.12 |
| Repeat Loyalists | 458 | 0.49% | 28,408.31 | 0.21% | 62.03 |

High-value segments (50.0% of customers) generate 83.3% of revenue.
Low-Value One-Time customers are still 16.5% of revenue on volume alone —
not a segment to ignore entirely, but clearly lower priority than reactivation.

**Recommendation:** prioritize a win-back campaign for the 23,078
"Lapsed High-Value" customers before spending further on acquisition — they
represent R$5.46M in prior revenue at a known high purchase level, making
them a higher-probability return than a cold acquisition channel.

## 3. Seller risk is concentrated in a small group with high cancellation rates

The composite risk score weights cancellation rate 2x over late-delivery
rate, since a cancellation is a stronger reliability signal than a late
shipment. Scores computed only for sellers with 10+ orders, to avoid
small-sample noise.

| Seller ID | Orders | Revenue (R$) | Late % | Cancel % | Risk score | Category |
|---|---|---|---|---|---|---|
| 81783131... | 13 | 1,782.54 | 7.69% | 38.46% | 84.61 | High |
| b1b39487... | 18 | 24,699.19 | 50.00% | 11.11% | 72.22 | High |
| 973f2178... | 10 | 909.00 | 50.00% | 10.00% | 70.00 | High |

**Recommendation:** flag sellers with `composite_risk_score > 70` for manual
account review rather than automatic deactivation — the top seller has low
order volume (13) and may be recoverable with a support conversation.

---

## 4. Win-back opportunity sizing — Lapsed High-Value segment

**What this is:** an estimate of the revenue opportunity if the business
acts on Finding #1, sized using a published industry benchmark — not a
measured outcome. **What this is not:** proof the campaign works — that
requires actually running it against a held-out control group.

**Benchmark used:** published 2025–2026 e-commerce win-back campaign data
(Klaviyo-sourced, compiled by Eightx) reports program-level reactivation
averaging 12–20% for a well-run multi-touch campaign.

| Scenario | Reactivated customers | Incremental revenue (R$) | New segment revenue (R$) | Lift |
|---|---|---|---|---|
| Conservative (12%) | 2,769 | 654,979.26 | 6,113,889.38 | 12.0% |
| Optimistic (20%) | 4,616 | 1,091,868.64 | 6,550,778.76 | 20.0% |

*Note: the lift % matches the reactivation rate by construction — since
incremental revenue is derived directly from reactivated customers × average
spend, this is a consistency check on the formula, not an independent finding.*

**How to actually prove this once implemented:**
1. Split the segment into a treatment group (receives the win-back sequence)
   and a control group (receives nothing), matched on `avg_monetary_per_customer`
   and `recency_days`.
2. After the campaign window (30–45 days), measure actual reactivation rate
   in each group.
3. The *difference* between treatment and control reactivation is the true
   causal effect — not the treatment group's raw number, since some
   customers would have returned anyway.
4. Replace the projected numbers above with measured ones once available.

---

*Source: `notebooks/final_analytics.ipynb` (Spark SQL marts + pandas/matplotlib
visualization). Underlying data: `analytics_exports/dashboard/segment_summary.csv`,
`analytics_exports/seller_scorecard.csv`, `analytics_exports/dashboard/cohort_summary.csv`,
`analytics_exports/dashboard/winback_projection.csv`.*
