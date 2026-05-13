# 🛍️ Customer Behaviour Analysis

A comprehensive retail analytics project that explores customer shopping patterns, spending habits, and business performance using **SQL**, **Power BI**, and a strategic PowerPoint presentation.

---

## 📌 Project Overview

This project analyses a retail customer dataset to uncover actionable business insights — from revenue drivers and discount effectiveness to customer segmentation and loyalty patterns. The goal is to answer real business questions that help stakeholders make informed, data-driven decisions.

**Tools & Technologies**
- **SQL (T-SQL / SQL Server)** — data querying and business logic
- **Power BI** — interactive dashboards and visualisations
- **PowerPoint** — executive strategy presentation
- **Python / Kaggle** — dataset source

---

## 📁 Repository Structure

```
CustomerBehaviourAnalysis/
│
├── archive.zip                          # Raw dataset (CSV)
├── BusinessInsights.sql                 # 12 SQL business insight queries
├── Customer_behaviour_analysis.pbix     # Power BI dashboard
├── Report-Customer Behaviour Analysis.pdf  # Written analysis report
├── Retail_Revenue_Strategy.pptx         # Strategy presentation deck
└── README.md
```

---

## 📊 Dataset

The dataset is sourced from **Kaggle** and contains **3,900 retail customer records** across the following fields:

| Column | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `age` | Customer age |
| `gender` | Male / Female |
| `item_purchased` | Product name |
| `category` | Product category (e.g. Clothing, Footwear) |
| `purchase_amount` | Transaction value (USD) |
| `review_rating` | Customer rating (1–5 scale) |
| `subscription_status` | Subscribed / Not subscribed |
| `shipping_type` | Shipping method (Standard, Express, etc.) |
| `discount_applied` | Whether a discount was used (Yes / No) |
| `previous_purchases` | Number of past transactions |

---

## 🔍 Business Questions Answered

The SQL file addresses **12 key business questions**:

| # | Question | Technique |
|---|---|---|
| 1 | Which product category generates the highest revenue? | `GROUP BY`, `ORDER BY` |
| 2 | Are discounts actually increasing purchase value? | Conditional aggregation |
| 3 | What is total revenue by gender? | `GROUP BY` |
| 4 | Which customers used a discount yet spent above average? | Correlated subquery |
| 5 | What are the top & bottom 5 products by review rating? | `TOP N`, `AVG`, `ORDER BY` |
| 6 | How does shipping type affect average spend and revenue? | Multi-metric aggregation |
| 7 | Do subscribers spend more than non-subscribers? | `GROUP BY`, comparison |
| 8 | Which products have the highest discount usage rate? | `CASE WHEN`, percentage calc |
| 9 | How can customers be segmented by purchase history? | `CASE WHEN` segmentation |
| 10 | What are the top 3 products within each category? | CTE + `RANK() OVER (PARTITION BY)` |
| 11 | Are repeat buyers more likely to subscribe? | Window function percentage |
| 12 | What is the revenue contribution of each age group? | `CASE WHEN` age banding |

---

## 🧠 SQL Techniques Used

```sql
-- Customer segmentation with CASE WHEN
SELECT
    CASE
        WHEN previous_purchases = 0         THEN 'New Customer'
        WHEN previous_purchases BETWEEN 1 AND 15 THEN 'Returning Customer'
        ELSE 'Loyal Customer'
    END AS customer_segment,
    COUNT(*) AS customer_count
FROM customer_behaviour_analysis
GROUP BY ...

-- Top 3 products per category using CTE + Window Function
WITH CTE AS (
    SELECT
        category,
        item_purchased,
        COUNT(item_purchased) AS purchase_count,
        RANK() OVER (PARTITION BY category ORDER BY COUNT(item_purchased) DESC) AS RNK
    FROM customer_behaviour_analysis
    GROUP BY category, item_purchased
)
SELECT * FROM CTE WHERE RNK <= 3;
```

---

## 📈 Key Findings

> Full findings are detailed in `Report-Customer Behaviour Analysis.pdf`

- **Clothing** is the highest-revenue product category
- **Discounts** show mixed impact — they increase total volume but reduce average order value
- **Subscribed customers** generate significantly higher lifetime revenue than non-subscribers
- **Loyal customers** (16+ previous purchases) are more likely to be subscribers
- The **26–50 age band** contributes the largest share of total revenue
- **Express shipping** correlates with higher average spend per order

---

## 📊 Power BI Dashboard

The `.pbix` file contains an interactive dashboard covering:

- Revenue breakdown by category, gender, and age group
- Subscription vs non-subscription spend comparison
- Discount usage analysis across products
- Customer segmentation distribution
- Shipping type performance

> Open with **Power BI Desktop** (free download at [powerbi.microsoft.com](https://powerbi.microsoft.com))

---

## 📑 Strategy Presentation

`Retail_Revenue_Strategy.pptx` is an executive-ready slide deck translating the analysis into business recommendations, including:

- Pricing and discount strategy
- Subscription programme growth opportunities
- Targeted marketing by customer segment and age group

---

## 🚀 Getting Started

### Run the SQL queries

1. Import the CSV from `archive.zip` into SQL Server (or any compatible RDBMS)
2. Create a database:
   ```sql
   CREATE DATABASE customer_shopping_behavior;
   USE customer_shopping_behavior;
   ```
3. Create a table matching the dataset schema and import the CSV
4. Open and run `BusinessInsights.sql`

### View the dashboard

1. Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/downloads/)
2. Open `Customer_behaviour_analysis.pbix`
3. Update the data source path to point to your local CSV if prompted

---

## 📌 Project Highlights

- ✅ 12 business-driven SQL queries with real analytical value
- ✅ Advanced SQL: CTEs, window functions, subqueries, conditional aggregation
- ✅ Interactive Power BI dashboard with multiple report pages
- ✅ Executive summary in PDF and PowerPoint format
- ✅ Clean, reproducible analysis workflow

---

## 👤 Author

**Muhammad Taha**
- GitHub: [@MuhammadTaha-GH](https://github.com/MuhammadTaha-GH)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

*Dataset sourced from Kaggle. For educational and portfolio purposes.*
