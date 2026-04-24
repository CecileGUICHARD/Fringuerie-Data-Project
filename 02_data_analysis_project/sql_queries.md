# SQL Queries

This section highlights selected SQL analyses developed during the project.

Rather than listing many queries, the examples below illustrate four analytical themes:

- operational performance monitoring  
- transaction behavior analysis  
- category mix benchmark analysis  
- promotional uplift analysis

Together, they showcase aggregation logic, window functions, segmentation and KPI-oriented analysis.

---

## 1. Monthly performance: revenue, weight sold and opening days

```sql
SELECT
  DATE_TRUNC(Date, MONTH) AS month,
  FORMAT_DATE('%b %Y', DATE_TRUNC(Date, MONTH)) AS month_label,

  ROUND(SUM(turnover), 2) AS total_turnover,
  ROUND(SUM(weight), 2) AS total_weight,

  COUNT(DISTINCT Date) AS nb_opening_days

FROM `second-hand-insights.projet_wagon.combined_echos_sales`

GROUP BY
  month,
  month_label

ORDER BY month
```

### Purpose

This query aggregates La Fringuerie sales data by month in order to compare three operational indicators:

- monthly revenue
- monthly weight sold
- number of opening days

It was used to build a multi-metric performance view showing how sales activity evolves over time and how opening frequency may influence turnover and sold volume.

---

## 2. Monthly transaction behavior: basket, quantity and transaction volume

```sql
SELECT

DATE_TRUNC(Date, MONTH) AS month,
FORMAT_DATE('%b %Y', DATE_TRUNC(Date, MONTH)) AS month_label,

ROUND(AVG(qty),2) AS avg_quantity,

ROUND(AVG(turnover),2) AS avg_basket,

COUNT(DISTINCT id_transaction) AS transactions_count

FROM `second-hand-insights.projet_wagon.combined_echos_sales`

GROUP BY
month,
month_label

ORDER BY month
```

### Purpose

This query analyzes monthly transaction behavior through three complementary indicators:

- average number of items per transaction  
- average transaction amount (average basket)  
- monthly transaction volume

It was used to understand purchasing behavior over time, identify changes in basket composition, and explore whether transaction volume and basket value evolve together.

---

## 3. Best-selling sub-categories by gender ranking

```sql
WITH category_sales AS (

SELECT
    sub_category,
    gender,
    COUNT(product_id) AS nb_products_sold,
    ROW_NUMBER() OVER(
        PARTITION BY gender
        ORDER BY COUNT(product_id) DESC
    ) AS category_rank

FROM `second-hand-insights.projet_wagon.vc_cat_final`

WHERE sold = TRUE

GROUP BY
    sub_category,
    gender

)

SELECT
    gender,
    sub_category,
    nb_products_sold,
    category_rank

FROM category_sales

WHERE category_rank <= 3

ORDER BY
    gender,
    category_rank;
```


### Purpose

This query ranks the top three best-selling product sub-categories within each gender segment using a window function.

It was used to:

- identify strongest-performing categories by gender  
- compare female and male assortment patterns  
- support benchmark-inspired category mix analysis  
- inform assortment recommendations for La Fringuerie

Using `ROW_NUMBER()` makes it possible to rank categories inside each gender segment rather than only ranking globally.

---

## 4. Impact of commercial operations on basket size and item quantity

```sql
SELECT

offer_event_yes_corrected AS operation_type,

ROUND(AVG(turnover),2) AS avg_basket,

ROUND(AVG(qty),2) AS avg_items_per_transaction,

COUNT(DISTINCT id_transaction) AS transactions_count

FROM `second-hand-insights.projet_wagon.combined_echos_sales`

GROUP BY
operation_type

ORDER BY
CASE
WHEN operation_type='opération commerciale' THEN 1
WHEN operation_type='événement' THEN 2
WHEN operation_type='offre spéciale' THEN 3
WHEN operation_type='aucune opération commerciale' THEN 4
END
```

### Purpose

This query compares transaction behavior across commercial operation types using a cleaned and standardized operation variable.

It was used to analyze:

- average basket value by promotion type  
- average number of items per transaction  
- transaction volume by operation type

The objective was to assess whether promotional activity (events or special offers) is associated with higher basket value or larger baskets compared with regular activity.

---

## SQL Techniques Demonstrated

Examples in this section include:

- Aggregations (`SUM`, `AVG`, `COUNT`)
- `GROUP BY`
- Window functions (`ROW_NUMBER`)
- Common Table Expressions (CTEs)
- Segmentation analysis
- Time series aggregation
- Ranking logic

These examples illustrate how SQL was used not only for extraction, but for analytical reasoning and business insight generation.