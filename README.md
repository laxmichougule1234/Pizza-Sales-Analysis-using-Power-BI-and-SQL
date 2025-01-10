# Pizza Sales Analysis

This repository contains the Pizza Sales Analysis project, which includes SQL queries for analyzing pizza sales data and a Power BI dashboard file for visualizing the insights. 

## Project Structure

```
PizzaSalesAnalysis/
├── README.md
├── SQL/
│   └── pizza_sales_queries.sql
├── PowerBI/
│   └── Project1.pbix
└── LICENSE (optional)
```

## Files

### SQL
- **pizza_sales_queries.sql**: Contains SQL queries for various Key Performance Indicators (KPIs) and other analytical insights, including revenue, order trends, and top-performing items.

### Power BI
- **Project1.pbix**: A Power BI report visualizing the pizza sales data.

## Features

- SQL queries for:
  - Total Revenue
  - Average Order Value
  - Total Pizzas Sold
  - Order Trends (Daily and Monthly)
  - Top/Bottom Performing Pizzas (by Revenue, Quantity, and Orders)
  - Percentage of Sales by Pizza Category and Size

- Power BI dashboard for:
  - Interactive data visualization.
  - Key metrics and trends at a glance.

## Prerequisites

To use the files in this repository, ensure you have the following:

- **SQL Database**: A database containing a table named `pizza_sales` with relevant data.
- **Power BI Desktop**: To open and explore the `.pbix` file.

## Usage

### SQL Queries
1. Import the `pizza_sales_queries.sql` file into your preferred SQL client.
2. Run the queries against your database to generate insights.

### Power BI Report
1. Open `Pizza_Sales.pbix` in Power BI Desktop.
2. Update the data source if needed to connect to your database.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any suggestions or improvements.



## Author

Laxmi Basavaraj Chougule - Aspiring Data Scientist

---

### Contact

For queries or feedback, please contact laxmichougule01@gmail.com

---

### SQL Queries
```sql
-- A. KPI's

-- 1. Total Revenue
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

-- 2. Average Order Value
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;

-- 3. Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;

-- 4. Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;

-- 5. Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales;

-- B. Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);

-- C. Monthly Trend for Orders
SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date);

-- D. % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;

-- E. % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;

-- F. Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;

-- G. Top 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;

-- H. Bottom 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;

-- I. Top 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;

-- J. Bottom 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;

-- K. Top 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;

-- L. Bottom 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
```
