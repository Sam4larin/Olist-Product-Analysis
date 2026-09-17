# Olist Product Analysis: Understanding the Growth Problem

Olist grew through a broad range of product categories, but the customer base showed very little repeat purchasing.

This analysis looks at the business behind that pattern: **the customer journey, retention, product mix, and category economics**.

Using 99,441 orders from Olist's Brazilian e-commerce dataset (2016–2018), I analysed the data around four business questions.

![Retention Curve](assets/retention_curve.png)

## Business Questions

* **Where is the customer journey breaking down?**
* **How strong is repeat purchasing after the first order?**
* **Which product categories create opportunities for repeat purchases and higher order value?**
* **Where do high-value categories create margin or fulfilment concerns?**

---

# What I Found

## 1. The customer journey was largely completed successfully

**97% of orders were delivered successfully**, with no Brazilian state falling below 95% delivery completion.

Of delivered orders, 91.9% arrived before the estimated delivery date, while **6.8% missed the estimated date entirely**.

The main order drop-off occurred around **payment approval and carrier stages**, accounting for roughly 3% of orders.

### Business insight

Delivery performance was relatively consistent across the market, so the larger growth opportunity sits beyond basic order fulfilment.

---

## 2. Repeat purchasing was extremely low

Average **month-1 retention was just 0.34%**.

Across customer cohorts, retention remained around **0.20 - 0.27% in later months**, with no meaningful recovery.

The pattern was consistent across cohorts from 2017 through mid-2018.

At the same time, **38 of 52 product categories had average review scores above 4.0/5**.

### Business insight

Customer satisfaction and repeat purchasing were not moving together.

The product mix provides an important explanation.

Olist's largest categories included:

* Bed & Bath - **9,167 orders**
* Sports & Leisure - **7,491**
* Furniture & Decor - **6,213**

These are largely durable products, where customers naturally purchase less frequently.

---

## 3. The categories with repeat-purchase potential represented very little of the marketplace

Consumable categories such as food, drinks, and pet products accounted for **less than 2.5% of total orders**.

| Category | Orders |
| -------- | -----: |
| Pet Shop |  1,682 |
| Food     |    435 |
| Drinks   |    284 |

These categories have a natural purchase cycle that could create more opportunities for customers to return.

There was also evidence of demand for higher-value products.

The **Computers** category averaged **$1,252 per order**, compared with a platform average of approximately $160, while maintaining a **4.24/5 review score**.

However, it generated only **176 orders across two years**.

### Business insight

The product mix contained two areas worth investigating:

**Repeat-purchase categories** that could create more frequent customer activity.

**High-value categories** that could increase the value of individual purchases.

---

## 4. Higher-value categories also need to be evaluated against fulfilment cost

Some high-value categories carried significantly higher freight costs.

| Category          | Average Order Value | Average Freight |
| ----------------- | ------------------: | --------------: |
| Office Furniture  |                $264 |          $40.71 |
| Home Appliances 2 |                $510 |          $44.61 |

These categories generate more value per order, but their shipping costs are also materially higher.

### Business insight

Category expansion should consider both **revenue potential and fulfilment economics**.

A high AOV alone does not show whether a category is commercially attractive.

---

# What This Means for the Business

The analysis points to a product-mix opportunity where Olist had a large base of customers completing purchases and generally positive product experiences, but the marketplace was heavily weighted toward products that customers do not need to buy frequently.

At the same time, categories with natural repeat-purchase behaviour represented a very small share of orders, while some high-value categories had limited scale.

This creates several areas for a product or commercial team to investigate:

* Cross-selling complementary products after high-value purchases
* Expanding categories with natural repeat-purchase cycles
* Understanding whether limited high-value category volume comes from demand or seller supply
* Evaluating category growth alongside freight and fulfilment costs

The next step would be to test whether changing the **product mix and cross-sell opportunities** can increase repeat purchasing without creating disproportionate fulfilment costs.

---

# Analysis

The project combines three focused analyses:

### Customer Journey

Order progression from **placed - approved - carrier - delivered**, including delivery performance and regional comparisons.

### Customer Retention

Monthly cohort analysis using `customer_unique_id` to measure repeat purchasing after the first order.

### Category Performance

Comparison of product categories using **order volume, average order value, review score, freight cost, and payment behaviour**.

---
## Charts
![Cohort Heatmap](assets/cohort_retention_heatmap.png)
**Cohort Retention Heatmap** - each row is an acquisition cohort,
each column is months since first purchase. Dark red = near-zero retention.

# Technical

**SQL + DuckDB**

* Multi-table joins
* Funnel analysis
* Category segmentation
* Aggregation

**Python / pandas**

* Cohort construction
* Retention calculations
* Cohort matrix

**Matplotlib / Seaborn**

* Retention curve
* Cohort heatmap

The full analysis can be reproduced with:

```bash
python scripts/run_all.py
```

---

# Project Structure

```text
olist-product-analysis/
├── assets/
│   ├── cohort_retention_heatmap.png
│   └── retention_curve.png
├── data/
├── sql/
│   ├── funnel_analysis.sql
│   └── segment_analysis.sql
├── python/
│   └── cohort_retention.py
├── scripts/
│   └── run_all.py
├── requirements.txt
└── README.md
```

## Data

Olist Brazilian E-Commerce dataset
**99,441 orders | September 2016 – October 2018**

The analysis uses Olist's relational datasets covering customers, orders, products, payments, reviews, and delivery information.

### Limitations

Retention analysis uses `customer_unique_id` to identify returning customers. Revenue figures use `payment_value`, which includes freight. Later 2018 cohorts have less follow-up time, and retention analysis covers delivered orders.
