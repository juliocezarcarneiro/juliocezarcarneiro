---
title: Running totals and rankings in SQL with window functions
summary: Two window functions answer "how are we tracking this month" and "what are our best sellers" without a single subquery.
tags: [sql]
---

Two questions come up in almost every sales review: *how are sales tracking month to date*, and *which products sell best*. SQL window functions answer both in one query.

Assume a table `daily_product_sales` with one row per product per day, and the columns `sale_date`, `product`, `qty` and `revenue`.

```sql
SELECT
    sale_date,
    product,
    revenue,
    SUM(revenue) OVER (
        PARTITION BY product
        ORDER BY sale_date
    ) AS revenue_month_to_date,
    RANK() OVER (
        PARTITION BY sale_date
        ORDER BY revenue DESC
    ) AS rank_that_day
FROM daily_product_sales
WHERE sale_date >= DATE_TRUNC('month', CURRENT_DATE)
ORDER BY sale_date, rank_that_day;
```

## How it works

- `SUM(...) OVER (PARTITION BY product ORDER BY sale_date)` adds up revenue for each product, day by day. Each row shows the running total up to that date.
- `RANK() OVER (PARTITION BY sale_date ORDER BY revenue DESC)` ranks products within each day. Rank 1 is that day's best seller.
- Unlike `GROUP BY`, window functions keep every row, so you get the detail and the total side by side.

## Where to use it

Put this behind a simple chart and anyone can see, every morning, whether a product is on pace and which ones carry the day.
