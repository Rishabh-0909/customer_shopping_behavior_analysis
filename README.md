# 🛍️ Customer Shopping Behavior Analytics

<p align="center">
  <b>End-to-end customer analytics project using Python, PostgreSQL, SQL & Power BI</b><br>
  <i>From raw shopping data to actionable customer and revenue insights.</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-Data%20Cleaning%20%26%20EDA-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PostgreSQL-Data%20Storage-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/SQL-Business%20Analysis-4479A1?style=for-the-badge&logo=postgresql&logoColor=white" alt="SQL">
  <img src="https://img.shields.io/badge/Power%20BI-Interactive%20Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="MIT License">
</p>

---

## 📌 Project Overview

**Customer Shopping Behavior Analytics** is an end-to-end data analytics project built to understand purchasing patterns, customer segments, subscription behavior, product performance, discounts, shipping preferences, and revenue contribution.

The project starts with a raw customer shopping dataset and takes it through:

> **Raw Data → Data Cleaning → Feature Engineering → PostgreSQL → SQL Analysis → Power BI Dashboard → Business Insights**

The goal is to demonstrate a practical analytics workflow rather than simply produce a dashboard: the same dataset is cleaned and transformed in Python, stored in PostgreSQL, interrogated using business-focused SQL queries, and finally presented through an interactive Power BI report.

---

## 🎯 Business Questions

The analysis addresses questions such as:

- 💰 How does revenue differ between male and female customers?
- 🏷️ Which customers use discounts but still spend above the overall average?
- ⭐ Which products have the highest average review ratings?
- 🚚 How do average purchase amounts compare across shipping types?
- 🔔 Do subscribers spend more than non-subscribers?
- 🏷️ Which products have the highest discount-purchase rates?
- 👥 How can customers be segmented using previous purchase history?
- 🛒 What are the top products within each category?
- 🔁 Are repeat buyers also more likely to subscribe?
- 📊 Which age groups contribute the most revenue?

---

## 📊 Dataset

The dataset contains **3,900 customer purchase records** and **18 original attributes**.

### Key fields

| Field | Description |
|---|---|
| `Customer ID` | Unique customer identifier |
| `Age` | Customer age |
| `Gender` | Customer gender |
| `Item Purchased` | Purchased product |
| `Category` | Product category |
| `Purchase Amount (USD)` | Purchase value |
| `Location` | Customer location |
| `Size` | Purchased size |
| `Color` | Product color |
| `Season` | Purchase season |
| `Review Rating` | Product/customer review rating |
| `Subscription Status` | Subscription membership status |
| `Shipping Type` | Shipping method |
| `Discount Applied` | Whether a discount was applied |
| `Promo Code Used` | Whether a promo code was used |
| `Previous Purchases` | Number of previous purchases |
| `Payment Method` | Payment method |
| `Frequency of Purchases` | Customer purchase frequency |

---

## 🧹 Data Preparation

The Python notebook performs the main preprocessing and feature engineering steps.

### Missing-value treatment

Missing `Review Rating` values are filled using the **median review rating within the corresponding product category**.

This preserves category-level differences instead of applying one global median to every missing value.

### Column standardization

Column names are converted to a cleaner SQL/Python-friendly format:

```text
Purchase Amount (USD)
        ↓
purchase_amount
```

### Feature engineering

Two analytical features are created:

#### `age_group`

Customers are divided into four age groups using quartiles:

- Young adult
- Adult
- Middle-aged
- Senior

#### `purchase_frequency_days`

Categorical purchase frequencies are converted into approximate day intervals:

```text
Weekly          → 7 days
Fortnightly     → 14 days
Bi-Weekly       → 14 days
Monthly         → 30 days
Quarterly       → 90 days
Every 3 Months  → 90 days
Annually        → 365 days
```

The redundant `promo_code_used` column is then removed from the analysis dataset.

---

## 🗄️ PostgreSQL Pipeline

After preprocessing, the transformed DataFrame is loaded into PostgreSQL as the:

```text
customer
```

table.

The project therefore demonstrates the transition from local analytical processing to a relational database workflow.

> **Security note:** database credentials are intentionally **not** included in this repository. If you recreate the notebook, use environment variables or a local configuration file rather than hard-coding credentials.

---

## 🔎 SQL Analysis

The SQL file contains **10 business-oriented analytical queries** covering:

1. Revenue by gender
2. Discount users with above-average purchases
3. Top 5 products by average rating
4. Standard vs Express shipping spend
5. Subscriber vs non-subscriber spending
6. Products with the highest discount rates
7. New / Returning / Loyal customer segmentation
8. Top 3 products within each category
9. Repeat buyers vs subscription status
10. Revenue contribution by age group

### Example

```sql
SELECT subscription_status,
       COUNT(customer_id) AS total_customers,
       ROUND(AVG(purchase_amount), 2) AS avg_spend,
       ROUND(SUM(purchase_amount), 2) AS total_revenue
FROM customer
GROUP BY subscription_status
ORDER BY total_revenue, avg_spend DESC;
```

This turns a raw customer table into a directly interpretable business question: **how does subscription status relate to customer spending and revenue?**

---

## 📈 Power BI Dashboard

The Power BI report contains a one-page **Customer Behavior Dashboard** designed around quick executive-level exploration.

### Dashboard components

**KPI cards**
- 👥 Number of Customers
- ⭐ Average Review Rating
- 💵 Average Purchase Amount

**Visual analysis**
- Subscription status distribution
- Revenue by product category
- Customer count by product category
- Revenue by age group
- Customer count by age group

**Interactive slicers**
- Subscription Status
- Gender
- Category

This allows users to move from a high-level view into targeted customer segments without changing the underlying analysis.

---

## 💡 Key Dataset Observations

Based on the processed dataset:

| Metric | Value |
|---|---:|
| Customers / records | **3,900** |
| Total revenue | **$233,081** |
| Average purchase | **$59.76** |
| Average review rating | **3.75 / 5** |
| Product categories | **4** |
| Locations | **50** |
| Products | **25** |

### Revenue distribution

**Gender**

- **Male:** $157,890
- **Female:** $75,191

**Product category**

- **Clothing:** $104,264
- **Accessories:** $74,200
- **Footwear:** $36,093
- **Outerwear:** $18,524

**Age group**

- **Young adult:** $62,143
- **Middle-aged:** $59,197
- **Adult:** $55,978
- **Senior:** $55,763

These figures are descriptive observations from the supplied dataset, not claims about customer behavior outside this dataset.

---

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| 🐍 **Python / Pandas** | Data cleaning & feature engineering |
| 🐘 **PostgreSQL** | Relational data storage |
| 🧮 **SQL** | Business analysis & segmentation |
| 📊 **Power BI** | Interactive dashboard & visualization |
| 📓 **Jupyter Notebook** | Reproducible analysis workflow |
| 📁 **CSV** | Source dataset |

---

## 📁 Repository Structure

```text
customer-shopping-behavior/
│
├── 📊 customer_behavior_dashboard.pbix
│   └── Power BI dashboard
│
├── 📓 customer_shopping_behavior.ipynb
│   └── Data cleaning + feature engineering + PostgreSQL loading
│
├── 🗃️ customer_shopping_behavior.sql
│   └── Business analysis queries
│
├── 📄 customer_shopping_behavior.csv
│   └── Raw customer shopping dataset
│
├── 📜 LICENSE
│   └── MIT License
│
└── 📖 README.md
    └── Project documentation
```

---

## 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/customer-shopping-behavior.git
cd customer-shopping-behavior
```

### 2. Install Python dependencies

```bash
pip install pandas sqlalchemy psycopg2-binary jupyter
```

### 3. Run the notebook

Open:

```text
customer_shopping_behavior.ipynb
```

Make sure the CSV file is in the same working directory.

### 4. Configure PostgreSQL

Create a PostgreSQL database, for example:

```text
customer_behavior
```

Then configure your local connection details.

**Do not commit passwords or credentials to GitHub.**

### 5. Execute the SQL analysis

Run:

```text
customer_shopping_behavior.sql
```

against the PostgreSQL database containing the `customer` table.

### 6. Open the Power BI dashboard

Open:

```text
customer_behavior_dashboard.pbix
```

Refresh the data/model if required and use the slicers to explore customer segments.

---

## 🧠 What This Project Demonstrates

This project showcases practical skills across the full analytics pipeline:

- Data cleaning
- Missing-value treatment
- Feature engineering
- Exploratory data analysis
- SQL aggregation
- CTEs
- Window functions
- Customer segmentation
- Revenue analysis
- PostgreSQL integration
- Dashboard design
- Business-question formulation
- Data storytelling

It is particularly useful as a portfolio project because it connects **technical data work with business-facing insights** rather than treating visualization as a standalone task.

---

## 🔮 Potential Extensions

Future versions could extend the project with:

- 📈 Customer Lifetime Value (CLV)
- 🔮 Purchase/revenue forecasting
- 🧠 RFM customer segmentation
- 🎯 Customer churn analysis
- 🏷️ Discount effectiveness analysis
- 📍 Geographic revenue analysis
- 💳 Payment-method behavior
- 📅 Seasonal purchasing trends
- 🤖 Customer propensity modeling
- 📊 Automated Power BI refresh pipeline

---

## 📜 License

This project is licensed under the **MIT License**.

See [`LICENSE`](LICENSE) for the full license text.

---

## ⭐ If You Found This Useful

If this project helped you understand an analytics workflow, feel free to **star ⭐ the repository** and explore the notebook, SQL analysis, and Power BI dashboard.

<p align="center">
  <b>Built with Python • SQL • PostgreSQL • Power BI</b>
</p>
