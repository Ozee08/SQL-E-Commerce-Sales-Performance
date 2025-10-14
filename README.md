# SQL-E-Commerce-Sales-Performance Analysis

## Project Overview

This project analyzes real-world **E-Commerce transactional data** from a UK-based online retailer. Using **SQL** for querying and **Python** for visualization, it explores customer behavior, sales trends, and revenue growth over time.

The project simulates a real-life analytics task where a data analyst is expected to clean raw data, store it in a database, and derive actionable insights for business growth.

---

## Objectives

- Extract and analyze sales performance using SQL.

- Identify revenue patterns and month-to-month growth rates.

- Discover the most valuable customers and top-selling products.

- Visualize KPIs using Python (Matplotlib & Seaborn).

--- 

## Tech Stack

| Tool                                     | Purpose                                                                                   |
| ---------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Python (Pandas, Matplotlib, Seaborn)** | Data cleaning, analysis, and visualization                                                |
| **SQLite**                               | SQL querying and database management                                                      |
| **Google Colab**                         | Development environment                                                                   |
| **Kaggle Dataset**                       | [E-Commerce Data (Online Retail)](https://www.kaggle.com/datasets/carrie1/ecommerce-data) |

---

## Dataset Description

The dataset contains over **500,000 transaction records** from December 2010 to December 2011.

### Key Columns:

| Column        | Description                |
| ------------- | -------------------------- |
| `InvoiceNo`   | Unique transaction number  |
| `StockCode`   | Product/item code          |
| `Description` | Product name               |
| `Quantity`    | Number of units sold       |
| `InvoiceDate` | Date of purchase           |
| `UnitPrice`   | Price per item             |
| `CustomerID`  | Unique customer identifier |
| `Country`     | Country of purchase        |

---

## Data Cleaning Steps

**1.** Removed missing `CustomerID` values

**2.** Filtered out negative or zero quantities and prices

**3.** Converted `InvoiceDate` to a datetime format

**4.** Created a new column `TotalPrice = Quantity × UnitPrice`

After cleaning, the data was saved into an SQLite database named `ecommerce.db`.

---

## SQL Analysis
## 1. Monthly Revenue Trend

This query calculates total monthly revenue across all transactions.

```sql
SELECT 
    strftime('%Y-%m', InvoiceDate) AS month,
    ROUND(SUM(TotalPrice), 2) AS monthly_revenue
FROM transactions
GROUP BY month
ORDER BY month;
```
![Monthly Revenue Trend](E-commerce%20Sales/Project%20Images/SQL.Python%201.png)

**Insight:** Reveals monthly sales performance and seasonal patterns.

---

## 2. Monthly Growth Rate

Measures the percentage growth in revenue from one month to the next using a SQL window function.

```sql
WITH revenue_cte AS (
  SELECT 
      strftime('%Y-%m', InvoiceDate) AS month,
      SUM(TotalPrice) AS revenue
  FROM transactions
  GROUP BY month
)
SELECT 
    month,
    revenue,
    ROUND(
      (revenue - LAG(revenue) OVER (ORDER BY month)) * 100.0 /
       LAG(revenue) OVER (ORDER BY month), 2
    ) AS growth_rate
FROM revenue_cte;
```
![Monthly Revenue Trend](E-commerce%20Sales/Project%20Images/SQL.Python%202.png)

**Insight:** Identifies months of strong performance or decline.

---

## 3. Top 10 Best-Selling Products

Finds the products that contributed the most to total revenue.

```sql
SELECT 
    Description AS product,
    ROUND(SUM(TotalPrice), 2) AS revenue
FROM transactions
GROUP BY product
ORDER BY revenue DESC
LIMIT 10;
```
![Monthly Revenue Trend](E-commerce%20Sales/Project%20Images/SQL.Python%203.png)

**Insight:** Helps the business focus on high-performing product lines.

---

## 4. Top 10 Countries by Revenue

Analyzes which countries generated the highest sales revenue.

```sql
SELECT 
    Country,
    ROUND(SUM(TotalPrice), 2) AS total_revenue
FROM transactions
GROUP BY Country
ORDER BY total_revenue DESC
LIMIT 10;
```
![Monthly Revenue Trend](E-commerce%20Sales/Project%20Images/SQL.Python%204.png)

**Insight:** Useful for geographic market segmentation and targeting.

---

## 5. Top 10 Customers by Spending

Identifies high-value customers by total amount spent.

```sql
SELECT 
    CustomerID,
    ROUND(SUM(TotalPrice), 2) AS total_spent
FROM transactions
GROUP BY CustomerID
ORDER BY total_spent DESC
LIMIT 10;
```

![Monthly Revenue Trend](E-commerce%20Sales/Project%20Images/SQL.Python%205.png)

**Insight:** Supports loyalty program design and personalized marketing.

---

## Visualizations

Python was used to visualize insights for better storytelling:

- **Line Chart:** Monthly revenue trends

- **Combo Chart:** Monthly revenue vs growth rate

- **Bar Charts:** Top products, countries, and customers by revenue

These visuals make the analysis clear and presentation-ready for stakeholders. 

---

## Key Insights

- The company experienced **strong revenue growth in Q4**, indicating seasonal demand.

- A small group of **loyal customers accounted for a large portion of total revenue**.

- **UK and Netherlands** emerged as dominant sales markets.

- **Top-selling products** contributed significantly to total revenue, suggesting a skewed product distribution.

--- 

## Conclusion

This project demonstrates how SQL and Python can work together to transform raw transactional data into strategic insights.
It reflects the workflow of a professional data analyst — from data cleaning and querying to visualization and storytelling.
The results can guide business decisions in pricing, inventory, and customer engagement.

--- 
