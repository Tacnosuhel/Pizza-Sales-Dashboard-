# Pizza Sales Analysis & Interactive BI Dashboard

An end-to-end data analytics portfolio project analyzing over 48,000 transactions from a pizza restaurant business. This project involves database architecture and metric validation using **Microsoft SQL Server (SSMS)**, paired with an interactive executive dashboard designed in **Microsoft Excel**.

---

## 📌 Project Overview

In data analytics, dashboards cannot rely on unverified front-end transformations alone. This project follows standard industry testing practices:
1. **Data Ingestion & SQL Verification:** Importing raw transaction records into MS SQL Server to write queries calculating high-level KPIs, sales distributions, and trend analysis.
2. **Data Pipeline & Modeling in Excel:** Connecting Excel directly to the SQL Server database (or flat file pipeline), executing data transformation/cleaning, building dynamic Pivot Tables, and establishing distinct count calculations.
3. **Interactive Visual Reporting:** Designing an executive-level dashboard featuring synchronized timeline slicers, custom color palettes, and structured business insight summaries.

---

## 🛠️ Tech Stack & Skills

- **Database:** Microsoft SQL Server (Transact-SQL / SSMS)
- **Spreadsheet / BI:** Microsoft Excel (Power Query, Pivot Tables, Pivot Charts, Timeline Slicers, Custom Number Formatting)
- **Analytical Concepts:** KPI Tracking, Trend Identification, Granularity Breakdown, Menu Engineering, Subqueries, Aggregations, Data Type Casting.

---

## 📊 Dataset Description

The analysis is performed on the 2015 pizza sales dataset (~48,620 line items across 21,350 unique orders):

| Field Name | Type | Description |
| :--- | :--- | :--- |
| `pizza_id` | INT | Primary key representing individual pizza items sold |
| `order_id` | INT | Transaction identifier (handles multi-item orders) |
| `pizza_name_id`| VARCHAR | Abbreviated pizza naming key |
| `quantity` | INT | Quantity of pizzas ordered per row item |
| `order_date` | DATE | Date the order was placed |
| `order_time` | TIME | Timestamp of the transaction |
| `unit_price` | DECIMAL | Price of a single pizza |
| `total_price`| DECIMAL | Total revenue generated (`quantity * unit_price`) |
| `pizza_size` | VARCHAR | Pizza size variant (Regular, Medium, Large, X-Large, XXL) |
| `pizza_category`| VARCHAR | Pizza category (Classic, Veggie, Supreme, Chicken) |
| `pizza_ingredients` | VARCHAR | Comma-separated list of ingredients |
| `pizza_name` | VARCHAR | Commercial name of the pizza item |

---

## 📈 Key Metrics & Problem Statements

### 1. Key Performance Indicators (KPIs)
- **Total Revenue:** Total sales generated across all orders.
- **Average Order Value (AOV):** Average spend per unique order.
- **Total Pizzas Sold:** Total count of individual pizza units purchased.
- **Total Orders:** Count of unique, distinct customer transactions.
- **Average Pizzas Per Order:** Average units per transaction (`Total Pizzas Sold / Total Orders`).

### 2. Granular Trends & Category Performance
- **Daily Trend for Total Orders:** Identify order volume fluctuations across days of the week.
- **Hourly Trend for Total Orders:** Isolate peak operating hours to optimize kitchen resources and staffing.
- **Percentage of Sales by Pizza Category & Size:** Calculate revenue contribution percentages.
- **Total Pizza Sold by Category:** Track inventory demand per category.
- **Top 5 Best Sellers vs. Bottom 5 Worst Sellers:** Evaluate highest- and lowest-performing menu items based on units sold.

---

## 💻 SQL Query Implementation & Logic

### Metric Validation Queries (Sample)

#### Key Performance Indicators (KPIs)
```sql
-- 1. Total Revenue
SELECT SUM(total_price) AS Total_Revenue 
FROM pizza_sales;

-- 2. Average Order Value
SELECT CAST(SUM(total_price) / COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS Avg_Order_Value 
FROM pizza_sales;

-- 3. Total Pizzas Sold
SELECT SUM(quantity) AS Total_Pizzas_Sold 
FROM pizza_sales;

-- 4. Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders 
FROM pizza_sales;

-- 5. Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
       CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_Per_Order
FROM pizza_sales;