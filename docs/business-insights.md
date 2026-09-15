# Business Insights — Olist E-Commerce Gold Layer

Findings from the gold-layer analytics marts (customer segmentation, seller
risk, cohort retention, lapse-reason segmentation), computed via Spark SQL
on ~93K delivered orders.

---

## 1. Retention, not acquisition, is the constraint

97% of customers place exactly one order. Month-1 repeat purchase rate
across 20 monthly cohorts is 0.48%, declining to 0.17% by month 12.

## 2. Revenue concentration is real but moderate

| Segment | Customers | % of customers | Revenue (R$) | % of revenue | Avg R$/customer |
|---|---|---|---|---|---|
| Recent High-Value | 23,600 | 25.28% | 5,556,234.68 | 42.02% | 235.43 |
| Lapsed High-Value | 23,078 | 24.72% | 5,458,910.12 | 41.29% | 236.54 |
| Low-Value One-Time | 46,222 | 49.51% | 2,177,945.00 | 16.47% | 47.12 |
| Repeat Loyalists | 458 | 0.49% | 28,408.31 | 0.21% | 62.03 |

## 3. Seller risk is concentrated in a small group with high cancellation rates

Composite risk score weights cancellation rate 2x over late-delivery rate.

**Caveat:** `order_status = 'canceled'` does not distinguish buyer-initiated
from seller-initiated cancellations. A meaningful share of cancellations may
be customer-driven (changed their mind, found it cheaper elsewhere) rather
than a seller failure, which would mean this score currently over-penalizes
some sellers. Treat the score as informative, not a clean causal signal of
seller reliability, until cancellation-initiator data is available.

## 4. Not all lapsed customers left for the same reason — and most left for no detectable reason at all

Splitting the Lapsed High-Value segment (23,078 customers) by whether their
**most recent order** showed a concrete negative signal (review score ≤2,
late delivery, or cancellation):

| Lapse bucket | Customers | % of segment | Revenue (R$) |
|---|---|---|---|
| No Detected Bad Experience | 19,273 | 83.51% | 4,463,614.96 |
| Bad Experience | 3,805 | 16.49% | 995,295.16 |

**Important framing note:** "No Detected Bad Experience" means exactly
that — no measurable platform-side failure occurred on their last order.
It does **not** mean these customers are loyal, satisfied, or forgetful.
The true reason (competitor activity, changed needs, price sensitivity,
genuinely forgetting) cannot be distinguished from transaction data alone.
The recommended messaging below is chosen specifically because it doesn't
presume a cause.

**Recommendations, split by bucket:**
- **No Detected Bad Experience (83.5% of the segment):** lead with a
  value-focused reminder, no discount. Published win-back guidance is
  explicit that leading with a discount for customers who have no
  demonstrated trust issue risks training them to wait for offers before
  engaging — a real, cited failure mode of blanket win-back campaigns.
- **Bad Experience (16.5% of the segment):** lead with acknowledgment of
  the issue, followed by a real incentive. This is where a discount is
  earned rather than wasted — it's addressing a specific, identified
  trust barrier, not a default first move.

**What's still a projection, not proof:** we do not have a bucket-specific
measured or published reactivation rate — only that messaging strategy
should differ. Applying the same 12–20% benchmark reactivation rate to both
buckets assumes they perform identically, which is exactly the flat
assumption this segmentation exists to question. The honest next step is
running the two messages as separate treatment arms and measuring each
bucket's actual reactivation rate independently.

---

## 5. Win-back opportunity sizing — Lapsed High-Value segment (overall)

| Scenario | Reactivated customers | Incremental revenue (R$) | Lift |
|---|---|---|---|
| Conservative (12%, benchmark-sourced) | 2,769 | 654,979.26 | 12.0% |
| Optimistic (20%, benchmark-sourced) | 4,616 | 1,091,868.64 | 20.0% |

This remains a segment-wide projection sized against a published industry
benchmark (12–20% program-level reactivation, Klaviyo/Eightx-sourced), not
a measured result. See Section 4 for how messaging — not the projected
rate — should differ within this segment.

**How to actually prove any of this once implemented:**
1. Split each bucket into a treatment group (receives the bucket-matched
   message) and a control group (receives nothing).
2. After the campaign window (30–45 days), measure actual reactivation
   rate in each of the four resulting groups.
3. The difference between treatment and control, within each bucket, is
   the true causal effect — not the treatment group's raw number.
4. Replace projected numbers with measured ones once available, and check
   whether the two buckets really do convert differently — if they don't,
   the segmentation was still worth testing, even if the messaging
   difference doesn't move the number.

---

*Source: `notebooks/04_sql_analytics.ipynb` (Spark SQL marts + pandas/matplotlib
visualization).*
