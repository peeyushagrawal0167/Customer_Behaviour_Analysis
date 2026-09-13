# Customer Shopping Behavior Analysis

An end-to-end data analysis project covering **Python (pandas)**, **SQL (PostgreSQL)**, and **Power BI**, built on a dataset of 3,900 individual customer purchase transactions.

The goal was to move from raw transactional data to decisions a retail team could actually act on — which customer segments and products are worth protecting, and where the loyalty and subscription programs are (and aren't) working.

## Project Structure

```
├── pandas.ipynb              # Data cleaning & feature engineering
├── sql_data.sql               # 10 business questions answered in SQL
├── data_analysis_project.pbix # Power BI dashboard (2 pages)
├── Customer_Shopping_Behavior_Analysis_Report.pdf  # Full write-up with results
└── README.md
```

## Dataset

- **Source:** [Customer Shopping Trends Dataset](https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset) (Kaggle)
- **Size:** 3,900 rows, 18 original columns → 19 after cleaning
- **Covers:** customer demographics, purchase details, discounts, shipping, ratings, and subscription behavior

## Workflow

**1. Python (pandas) — Clean & Engineer**
- Filled 37 missing `review_rating` values using each product category's own median
- Standardized all column names to snake_case
- Engineered `age_group` (quantile-based bins) and `purchase_frequency_days` (mapped from text frequency labels)
- Verified `discount_applied` and `promo_code_used` were identical, dropped the redundant column
- Loaded the cleaned DataFrame into PostgreSQL via SQLAlchemy

**2. SQL (PostgreSQL) — Ask Business Questions**
10 questions answered directly in SQL, using a range of techniques: subqueries, CTEs, window functions (`ROW_NUMBER() OVER (PARTITION BY ...)`), and conditional aggregation. Covers revenue comparisons, customer segmentation, product performance, and discount/shipping analysis.

**3. Power BI — Visualize & Decide**
A 2-page interactive dashboard with synced filters (subscription status, gender, season) and custom DAX measures (Total Revenue, VIP Customer Rate, Customer Loyalty Tier).
- **Page 1 — Overview:** headline KPIs, revenue by category, order value by age group, customer loyalty tier breakdown, decomposition tree
- **Page 2 — Merchandising, Fulfillment & Sentiment:** product performance scatter, shipping/rating distribution, discount impact analysis

## Key Findings

- The customer base is overwhelmingly **Loyal** (3,116 of 3,900 customers) — this is a mature customer base, not one in early acquisition
- **Subscribers don't spend more per order** than non-subscribers ($59.49 vs. $59.87 avg) — the subscription program isn't currently converting into higher-value baskets
- **Repeat buyers skew heavily toward non-subscribers** (2,518 vs. 958) — loyalty isn't translating into sign-ups
- Hats, Sneakers, Coats, Sweaters, and Pants each rely on discounts for **close to half their sales** — worth watching for margin erosion
- Revenue is spread fairly evenly across age groups — **behavioral segmentation (loyalty tier) is a stronger lever than age-based targeting**

Full methodology, all 10 SQL queries with results, and the complete write-up are in the [PDF report](./Customer_Shopping_Behavior_Analysis_Report.pdf).

## How to Reproduce

1. Download the dataset from the Kaggle link above
2. Run `pandas.ipynb` to clean the data and load it into a local PostgreSQL database
   - Create a `.env` file in the same folder with your own database credentials:
     ```
     DB_USERNAME=your_username
     DB_PASSWORD=your_password
     DB_HOST=localhost
     DB_PORT=5432
     DB_NAME=your_database
     ```
3. Run the queries in `sql_data.sql` against the loaded table
4. Open `data_analysis_project.pbix` in Power BI Desktop and point it at the same database to refresh the dashboard

## Tech Stack

Python (pandas) · PostgreSQL · SQLAlchemy · Power BI (DAX)
