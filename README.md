# Fringuerie Data Project

## Overview

This project focuses on the data analysis and operational tracking of **La Fringuerie**, a local second-hand textile activity run by the association *Les Échos Ludiques*.

It combines two complementary dimensions:

1. **A data analysis project** carried out during my Data Analytics training  
(SQL, KPI definition, exploratory analysis and Looker dashboarding)

2. **An operational data collection initiative** currently being structured for the association  
(Google Forms, Google Sheets, cash tracking and data quality logic)

This project illustrates a full data approach:

**Business need → Data quality → Analysis → Decision support**

---

## Project Context

La Fringuerie operates in a volunteer-based context with practical constraints:

- limited resources  
- manual tracking habits  
- non-technical users  
- fragmented operational information  
- need for simple and useful tools

This project emerged from two complementary needs:

- better understand activity performance through data analysis  
- improve how field data is collected and structured

The analytical project helped identify what should be measured.

The operational project aims to improve how those data are captured at the source.

---

## Business Problem

Several challenges were identified:

- limited visibility on sales performance  
- manually tracked information difficult to analyze  
- product categories not always structured for reporting  
- cash register monitoring requiring manual checks  
- lack of simple recurring indicators

This created a double need:

1. analyze available data to extract insights  
2. improve future data collection to make analysis more reliable

---

## Project Objectives

- Explore and analyze sales data
- Define meaningful KPIs
- Use SQL to aggregate and explore data
- Build dashboards to visualize insights
- Improve data collection logic
- Prepare cleaner data for future reporting

---

# Part 1 — Data Analysis Project

## Scope

This part was carried out during my Data Analytics training.

Main topics covered:

- SQL queries
- Aggregations and GROUP BY
- KPI definition
- Sales analysis
- Product category analysis
- Dashboarding with Looker
- Business recommendations

---

## Example business questions explored

- Which categories contribute most to sales?
- What indicators should be monitored?
- How does activity evolve over time?
- What operational recommendations can data support?

---

## Example KPIs

Examples of indicators used or identified:

- Total revenue
- Number of items sold
- Average basket
- Revenue by category
- Quantity by category
- Payment method distribution

---

## Example SQL logic

```sql
SELECT
    category,
    COUNT(*) AS sales_count,
    SUM(quantity) AS items_sold,
    SUM(amount) AS revenue
FROM sales
GROUP BY category
ORDER BY revenue DESC;
```

```sql
SELECT
    payment_method,
    SUM(amount) AS revenue
FROM sales
GROUP BY payment_method;
```

---

## Dashboarding (Looker)

The dashboard focused on:

- activity overview
- category analysis
- payment analysis
- operational recommendations

(Screenshots available in assets folder)

---

## Example recommendations

Examples of recommendations derived from analysis:

- improve tracking of product categories
- prioritize high-performing categories
- standardize key fields for future monitoring
- build simple recurring KPI tracking

---

# Part 2 — Operational Data Collection

## Objective

Extend the project into a practical field initiative:

Create a simple and reliable data collection process adapted to volunteers.

---

## Tools used

- Google Forms
- Google Sheets
- Spreadsheet formulas
- Data quality controls

---

## Main focus

Work in progress around:

- cash register opening / closing tracking
- sales collection forms
- payment method tracking
- product category structuring
- preparation of cleaner operational data

---

## Cash tracking logic

Example reconciliation logic:

```text
Opening cash + cash sales = expected closing cash
```

Observed closing amount can then be compared to expected amount and flagged if needed.

---

## Example data quality rules

Examples of controls:

- every closing should match an opening
- totals rebuilt from denomination counts
- payment methods cannot be empty
- categories standardized for analysis
- multi-select categories transformed into structured fields

Example:

```text
Original:
Femme, Accessoires

Structured:
femme = 1
accessoires = 1
homme = 0
enfant = 0
```

---

# Data Workflow

```text
Operational activity
↓
Raw data collection
↓
Data cleaning and structuring
↓
SQL analysis / KPI definition
↓
Dashboard and recommendations
↓
Improved operational tracking
```

---

# Repository Structure

```text
01_business_context
02_data_analysis_project
03_operational_data_collection
04_assets
05_sample_data
06_roadmap
```

---

# Tools & Skills Demonstrated

## Technical tools

- SQL
- Looker / Looker Studio
- Google Forms
- Google Sheets

## Data skills

- business analysis
- KPI definition
- aggregation
- data cleaning
- dashboarding
- data quality controls
- operational process design

---

# Current Status

## Completed

- Business context analysis
- SQL analysis
- KPI definition
- Looker exploration
- Initial recommendations

## In progress

- Operational data collection structuring
- Cash register control workflow
- Google Sheets cleaning logic
- Data quality rules

---

# Next Steps

- Finalize operational data collection process
- Strengthen sample datasets
- Extend KPI monitoring layer
- Enrich dashboarding
- Explore automation opportunities

---

# Key Learning

This project reinforced a central idea:

A data project does not start with a dashboard.

It starts with:

- understanding the business need
- structuring reliable data
- defining useful indicators
- then visualizing insights

---

## Data Privacy

All examples in this repository are anonymized or fictionalized.

No personal or sensitive information is shared.

---

## Author

Cécile Guichard  
Data Analyst
