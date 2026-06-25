# 💳 Credit Card Analytics — SQL Project

A complete end-to-end SQL analysis of a credit card customer dataset. This project covers data quality checks, KPI reporting, customer segmentation, churn analysis, and behavioral insights — all written in pure SQL.

---

## 📌 Project Overview

Financial institutions generate massive amounts of customer data. This project simulates a real-world analytics workflow to extract business insights from a credit card customer database, focusing on:

- Understanding who the customers are
- Identifying customers at risk of churning
- Discovering spending patterns and credit behavior
- Segmenting customers for targeted strategies

---

## 🗂️ Dataset

**Table:** `cards`  
**Database:** `credit_card`

| Column | Description |
|---|---|
| `clientnum` | Unique customer identifier |
| `attrition_flag` | Whether the customer churned (`Attrited Customer` / `Existing Customer`) |
| `customer_age` | Customer's age |
| `gender` | Customer's gender |
| `education_level` | Highest education level |
| `marital_status` | Marital status |
| `income_category` | Annual income bracket |
| `card_category` | Type of card (Blue / Silver / Gold / Platinum) |
| `credit_limit` | Credit limit on the card |
| `total_trans_amt` | Total transaction amount |
| `avg_utilization_ratio` | Average credit utilization ratio |

---

## 🧹 Data Quality Checks

Before any analysis, the following checks were performed:

| Check | Query Goal |
|---|---|
| **Total Records** | Count all rows in the dataset |
| **Duplicate Detection** | Find `clientnum` values that appear more than once |
| **Null Values** | Check for missing `Education_Level`, `Marital_Status`, `Income_Category` |
| **Unknown/Placeholder Values** | Audit distinct values in categorical columns |
| **Negative Values** | Validate `credit_limit` and `total_trans_amt` are non-negative |

---

## 📊 KPIs & Business Metrics

```sql
-- Total Customers
SELECT COUNT(*) AS total_customers FROM cards;

-- Churn Rate (%)
SELECT SUM(CASE WHEN attrition_flag = 'Attrited Customer' THEN 1 ELSE 0 END)
       * 100.0 / COUNT(*) AS churn_rate
FROM cards;

-- Total Transaction Volume
SELECT SUM(total_trans_amt) AS total_transaction FROM cards;

-- Average Credit Limit
SELECT AVG(credit_limit) FROM cards;
```

---

## 🔍 Analysis Sections

### 1. Customer Demographics
- Gender distribution
- Education level breakdown
- Income category distribution
- Card category distribution

### 2. Churn Analysis
- Overall churn rate
- Churn by gender
- Churn by card type (with churn %)
- Churn rate by age group

### 3. Credit & Spending Behavior
- Top 10 highest credit limits
- Top 10 highest spending customers
- Most active customers by transaction volume
- Top spender per card category (using `ROW_NUMBER()` window function)

### 4. Customer Segmentation
- **Credit Utilization Segments:** Low (<0.3) / Medium (0.3–0.7) / High (>0.7)
- **Age Group Buckets:** 20–30 / 31–40 / 41–50 / 50+
- Average credit limit by card category

---

## 🧠 Key SQL Concepts Used

| Concept | Where Used |
|---|---|
| `GROUP BY` + `COUNT` | Demographics, distributions |
| `CASE WHEN` | Churn rate, segmentation, age groups |
| `HAVING` | Duplicate detection |
| `ORDER BY` + `LIMIT` | Top N customers |
| `WITH` (CTE) | Top spender per card category |
| `ROW_NUMBER()` | Window function for ranked partitions |
| Aggregate functions (`SUM`, `AVG`, `COUNT`) | KPIs |
| Conditional aggregation | Churn rates by segment |

---

## 📁 Project Structure

```
credit-card-analytics/
│
├── README.md
└── credit_card_analytics.sql    # All queries in one file
```

---

## 🚀 How to Run

1. **Set up MySQL** (or any compatible SQL engine)
2. **Import the dataset** into a table named `cards` inside the `credit_card` database
3. **Run the SQL file:**

```bash
mysql -u your_username -p credit_card < credit_card_analytics.sql
```

Or paste queries directly into **MySQL Workbench**, **DBeaver**, or any SQL client.

---

## 💡 Business Insights (Sample)

- The overall **churn rate** reveals how aggressively the bank needs to focus on retention
- **Blue cardholders** make up the majority of customers but may have a higher churn rate than premium tiers
- **High credit utilization** customers are power users but also carry higher financial risk
- Customers aged **40–50** tend to be the most financially active segment
- The **top 10 spenders** can be targeted for premium card upgrades

---

## 🛠️ Tools Used

- **MySQL** — Query execution
- **SQL** — Entire analysis written in pure SQL (no Python, no BI tools)

---

## 👤 Author

**[Your Name]**  
Aspiring Data Analyst | SQL • Python • Excel  
📧 [your.email@example.com]  
🔗 [LinkedIn Profile URL]

---

## ⭐ If you found this project useful, please give it a star!
