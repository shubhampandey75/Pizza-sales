# 🍕 Pizza Sales Analysis

An end-to-end data analysis project analyzing pizza sales performance using **MySQL** for data querying and **Excel** for interactive dashboarding.

---

## 📊 Dashboard Preview

![Pizza Sales Dashboard](dashboard.png)

---

## 📌 Project Overview

This project dives into a pizza restaurant's sales data to uncover trends around revenue, order patterns, customer behavior, and product performance. MySQL was used to extract and validate all KPIs, which were then visualized in an Excel dashboard for business reporting.

---

## 🔍 Key Insights

| Metric | Value |
|---|---|
| 💰 Total Revenue | $817,860 |
| 🛒 Total Orders | 21,350 |
| 🍕 Total Pizzas Sold | 49,574 |
| 💵 Avg Order Value | $38 |
| 📦 Avg Pizzas Per Order | 2.32 |

- **Busiest Days:** Friday and Saturday see the highest order volumes
- **Peak Hours:** Orders spike at **12:00 PM** and again between **4 PM – 8 PM**
- **Top Category:** Classic category leads in both total sales and total orders
- **Top Size:** Large pizzas contribute the most to revenue
- **Best Sellers:** The Classic Deluxe Pizza and Barbecue Chicken Pizza are top revenue generators
- **Worst Performer:** The Brie Carre Pizza sits at the bottom in both orders and revenue

---

## 🛠️ Tools & Technologies

- **MySQL** — Data extraction, KPI calculation, and trend analysis
- **Microsoft Excel** — Interactive dashboard with charts, slicers, and KPI cards

---

## 📁 Project Structure

```
pizza-sales-analysis/
│
├── pizza_sales_queries.sql     # All MySQL queries used for analysis
├── Pizza_Sales_Dashboard.xlsx  # Excel dashboard file
├── pizza_sales.csv             # Raw dataset
├── dashboard.png               # Dashboard screenshot
└── README.md
```

---

## 🗄️ SQL Queries Covered

**KPI Metrics**
```sql
-- Total Revenue
SELECT SUM(total_price) FROM pizza_sales;

-- Average Order Value
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Avg_order_value FROM pizza_sales;

-- Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;

-- Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_order FROM pizza_sales;

-- Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_pizza_per_order
FROM pizza_sales;
```

**Trend Analysis**
```sql
-- Daily Trend
SELECT DAYNAME(order_date) AS Order_day, COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales GROUP BY DAYNAME(order_date);

-- Hourly Trend
SELECT HOUR(order_time) AS Order_time, COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales GROUP BY HOUR(order_time) ORDER BY HOUR(order_time);
```

**Sales Breakdown**
```sql
-- % Sales by Category
SELECT pizza_category,
SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS Total_sales
FROM pizza_sales GROUP BY pizza_category;

-- % Sales by Size
SELECT pizza_size,
SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS Total_sales
FROM pizza_sales GROUP BY pizza_size;

-- Top/Bottom Sellers by Quantity
SELECT pizza_name, SUM(quantity) AS Total_pizza_sold
FROM pizza_sales GROUP BY pizza_name ORDER BY SUM(quantity) DESC;
```

---

## 📈 Dashboard Features

- KPI cards for Revenue, Orders, Units Sold, Avg Order Value, and Avg Pizzas Per Order
- Daily and Hourly order trend charts
- % Sales breakdown by pizza category (donut chart)
- % Sales breakdown by pizza size (pie chart)
- Units sold by category (bar chart)
- Top 5 Best Selling Pizzas
- Bottom 5 Worst Selling Pizzas
- Month and date slicer for time-based filtering

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/pizza-sales-analysis.git
   cd pizza-sales-analysis
   ```

2. Import the dataset into MySQL:
   ```sql
   CREATE DATABASE pizza_db;
   USE pizza_db;
   -- Then import pizza_sales.csv into a table named pizza_sales
   ```

3. Run the queries in `pizza_sales_queries.sql` using MySQL Workbench or any SQL client

4. Open `Pizza_Sales_Dashboard.xlsx` in **Microsoft Excel** to explore the dashboard

---

## 📂 Dataset

- **Source:** [Kaggle – Pizza Sales Dataset](https://www.kaggle.com/) *(update with actual link)*
- **Key Columns:** `order_id`, `order_date`, `order_time`, `pizza_name`, `pizza_category`, `pizza_size`, `quantity`, `total_price`

---
