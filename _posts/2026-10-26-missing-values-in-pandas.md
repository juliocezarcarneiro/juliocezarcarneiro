---
title: Handling missing values in pandas, without guessing
summary: Fill numbers with the median, categories with the most common value, and drop rows only when a key field is missing. Then write down why.
tags: [python, data-quality]
---

Missing values are normal in sales exports and supplier files. The mistake is filling them without thinking. A short rule set keeps it honest:

```python
# Numbers: the median is safer than the mean when there are outliers
df['unit_cost'] = df['unit_cost'].fillna(df['unit_cost'].median())

# Categories: use the most common value
df['category'] = df['category'].fillna(df['category'].mode()[0])

# Key fields: if we can't identify the row, drop it
df = df.dropna(subset=['order_id', 'order_date'])
```

## The rule behind each line

1. **Numbers get the median.** One unusually large order can drag the mean far from a normal day.
2. **Categories get the mode.** It's the least surprising guess.
3. **Rows without an ID or date are dropped.** You can't put them on a timeline or match them to anything.

## The step people skip

Write down what you filled and why, and count rows before and after. My [data cleaning template](https://github.com/juliocezarcarneiro/data-cleaning-template) saves that as a before/after report every time it runs.
