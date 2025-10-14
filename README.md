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

1. Removed missing CustomerID values

2. Filtered out negative or zero quantities and prices

3. Converted InvoiceDate to a datetime format

4. Created a new column TotalPrice = Quantity × UnitPrice

After cleaning, the data was saved into an SQLite database named ecommerce.db.

---

## SQL Analysis
## Monthly Revenue Trend

This query calculates total monthly revenue across all transactions.

```sql
SELECT 
    strftime('%Y-%m', InvoiceDate) AS month,
    ROUND(SUM(TotalPrice), 2) AS monthly_revenue
FROM transactions
GROUP BY month
ORDER BY month;
```
![Monthly Revenue Trend](./Project%20Images/SQL.Python%201.png)
