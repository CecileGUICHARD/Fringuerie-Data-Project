# SQL Queries

This section documents examples of SQL logic used during the data analysis project.

The queries are simplified and anonymized for portfolio purposes.

---

## 1. Revenue by product category

```sql
SELECT
    category,
    SUM(amount) AS total_revenue
FROM sales
GROUP BY category
ORDER BY total_revenue DESC;
```

### Purpose

This query identifies which product categories generate the most revenue.

---

## 2. Quantity sold by category

```sql
SELECT
    category,
    SUM(quantity) AS total_items_sold
FROM sales
GROUP BY category
ORDER BY total_items_sold DESC;
```

### Purpose

This query shows which categories are sold most frequently.

---

## 3. Revenue and quantity by category

```sql
SELECT
    category,
    SUM(quantity) AS total_items_sold,
    SUM(amount) AS total_revenue
FROM sales
GROUP BY category
ORDER BY total_revenue DESC;
```

### Purpose

This query combines volume and revenue to compare category performance.

---

## 4. Average basket

```sql
SELECT
    ROUND(SUM(amount) / COUNT(*), 2) AS average_basket
FROM sales;
```

### Purpose

This query calculates the average revenue per transaction.

---

## 5. Sales by payment method

```sql
SELECT
    payment_method,
    COUNT(*) AS number_of_transactions,
    SUM(amount) AS total_revenue
FROM sales
GROUP BY payment_method
ORDER BY total_revenue DESC;
```

### Purpose

This query analyzes how customers pay and helps prepare cash tracking.

---

## 6. Monthly revenue

```sql
SELECT
    DATE_TRUNC(date, MONTH) AS month,
    SUM(amount) AS monthly_revenue,
    SUM(quantity) AS monthly_items_sold
FROM sales
GROUP BY month
ORDER BY month;
```

### Purpose

This query tracks sales evolution over time.

---

## 7. Category share in total revenue

```sql
SELECT
    category,
    SUM(amount) AS category_revenue,
    ROUND(
        SUM(amount) / SUM(SUM(amount)) OVER () * 100,
        2
    ) AS revenue_share_percent
FROM sales
GROUP BY category
ORDER BY revenue_share_percent DESC;
```

### Purpose

This query calculates the percentage contribution of each category to total revenue.

---

## 8. Revenue by category and payment method

```sql
SELECT
    category,
    payment_method,
    SUM(amount) AS total_revenue
FROM sales
GROUP BY category, payment_method
ORDER BY category, total_revenue DESC;
```

### Purpose

This query gives a more detailed view of sales by both category and payment method.

---

## Notes

The objective of these queries was to:

- aggregate sales data
- compare categories
- define useful KPIs
- support dashboard creation
- translate data into operational insights