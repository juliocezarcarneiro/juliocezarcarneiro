---
title: Running totals and rankings by menu item in SQL
summary: Two window functions answer "how are we tracking this month" and "what are our best sellers" without a single subquery.
tags: [sql, hospitality]
---

Two questions come up in almost every restaurant review: *how are sales tracking month to date*, and *which items sell best*. SQL window functions answer both in one query.

Assume a table `daily_item_sales` with one row per item per day, and the columns `sale_date`, `menu_item`, `qty` and `revenue`.

```sql
SELECT
    sale_date,
    menu_item,
    revenue,
    SUM(revenue) OVER (
        PARTITION BY menu_item
        ORDER BY sale_date
    ) AS revenue_month_to_date,
    RANK() OVER (
        PARTITION BY sale_date
        ORDER BY revenue DESC
    ) AS rank_that_day
FROM daily_item_sales
WHERE sale_date >= DATE_TRUNC('month', CURRENT_DATE)
ORDER BY sale_date, rank_that_day;
```

## How it works

- `SUM(...) OVER (PARTITION BY menu_item ORDER BY sale_date)` adds up revenue for each item, day by day. Each row shows the running total up to that date.
- `RANK() OVER (PARTITION BY sale_date ORDER BY revenue DESC)` ranks items within each day. Rank 1 is that day's best seller.
- Unlike `GROUP BY`, window functions keep every row, so you get the detail and the total side by side.

## Where to use it

Put this behind a simple chart and a manager can see, every morning, whether an item is on pace and which dishes carry the day.
