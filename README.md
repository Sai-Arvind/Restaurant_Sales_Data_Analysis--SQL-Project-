# 🍽️ Restaurant Sales Data Analysis (SQL Project)

### 🌟 Project Summary
This project demonstrates proficiency in SQL for data analysis by exploring a restaurant's operational data. 
The analysis focuses on three key areas—**Menu Composition**, **Order Volume**, and **Customer Spending**—to provide actionable business intelligence.

The complete SQL code used for this analysis is available in the `restaurant_analysis.sql` file.

---

### 🔑 Key Analytical Questions

This analysis addresses the following core business questions:

#### 1. Menu Analysis
* What is the pricing range of menu items, and what is the average price per category?
* How many dishes are available in specialty categories (e.g., Italian)?

#### 2. Order Details Analysis
* What is the date range and total volume of orders recorded?
* Which orders were the largest by item count, and how many orders exceed 12 items?

#### 3. Customer Behavior Analysis (Cross-Table Analysis)
* Which menu items are the **most and least popular** sellers?
* Which orders generated the **highest revenue**?
* What food categories dominate the top-spending orders?

---
```

### 📂 Repository Structure
The project is structured for clarity, containing the two essential files for this analysis:

restaurant-sql-analysis/
├── restaurant_analysis.sql <-- Contains all 18 SQL queries.
└── README.md <-- This file.


### 🛠️ Technologies Used
* **SQL (MySQL/PostgreSQL)**: Primary language for data extraction and analysis.
* **Database Schema**: Assumes the existence of `menu_items` and `order_details` tables.
```
---

### 💡 Example Query: Identifying Top Spending Orders

```sql
SELECT od.order_id, SUM(mi.price) AS total_spend
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id
GROUP BY od.order_id
ORDER BY total_spend DESC
LIMIT 5;

---

## 💾 `restaurant_analysis.sql` https://mavenanalytics.io/data-playground/restaurant-orders 

USE restaurant_db;

-- ****************** MENU ITEMS ANALYSIS ******************

-- 1. View the menu_items table
SELECT * FROM menu_items;

-- 2. Number of items on the menu
SELECT COUNT(*) FROM menu_items;

-- 3. Least and most expensive menu items
SELECT 'Most Expensive' AS type, item_name, price
FROM menu_items
ORDER BY price DESC
LIMIT 1;

SELECT 'Least Expensive' AS type, item_name, price
FROM menu_items
ORDER BY price ASC
LIMIT 1;

-- 4. Total Italian dishes
SELECT COUNT(*)
FROM menu_items
WHERE category = 'Italian';

-- 5. Most and least expensive Italian dishes
SELECT *
FROM menu_items
WHERE category = 'Italian'
ORDER BY price DESC
LIMIT 1;

SELECT *
FROM menu_items
WHERE category = 'Italian'
ORDER BY price ASC
LIMIT 1;

-- 6. Dishes per category
SELECT category, COUNT(menu_item_id) AS num_dishes
FROM menu_items
GROUP BY category;

-- 7. Average dish price per category
SELECT category, ROUND(AVG(price), 2) AS avg_dish_price
FROM menu_items
GROUP BY category;

-- ****************** ORDER DETAILS ANALYSIS ******************

-- 1. View order_details table
SELECT * FROM order_details;

-- 2. Date range of orders
SELECT MIN(order_date) AS earliest_date, MAX(order_date) AS latest_date
FROM order_details;

-- 3. Total distinct orders
SELECT COUNT(DISTINCT order_id) AS total_orders
FROM order_details;

-- 4. Total items ordered
SELECT COUNT(*) AS total_items_ordered
FROM order_details;

-- 5. Orders with most items (Top 5)
SELECT order_id, COUNT(item_id) AS num_items
FROM order_details
GROUP BY order_id
ORDER BY num_items DESC
LIMIT 5;

-- 6. Orders with more than 12 items
SELECT COUNT(*) AS total_large_orders
FROM (
    SELECT order_id, COUNT(item_id) AS num_items
    FROM order_details
    GROUP BY order_id
    HAVING num_items > 12
) AS large_orders;

-- ****************** CUSTOMER BEHAVIOR ANALYSIS ******************

-- 1. Join menu_items and order_details
SELECT *
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id;

-- 2. Most ordered item
SELECT mi.item_name, mi.category, COUNT(od.order_details_id) AS num_purchases
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id
GROUP BY mi.item_name, mi.category
ORDER BY num_purchases DESC
LIMIT 1;

-- Least ordered item
SELECT mi.item_name, mi.category, COUNT(od.order_details_id) AS num_purchases
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id
GROUP BY mi.item_name, mi.category
ORDER BY num_purchases ASC
LIMIT 1;

-- 3. Top 5 highest revenue orders
SELECT od.order_id, SUM(mi.price) AS total_spend
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id
GROUP BY od.order_id
ORDER BY total_spend DESC
LIMIT 5;

-- 4. Category breakdown of highest spending order (Example: 440)
SELECT mi.category, COUNT(od.item_id) AS num_items_in_category
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id
WHERE od.order_id = 440
GROUP BY mi.category;

-- 5. Category breakdown for top 5 highest spend orders
SELECT mi.category, COUNT(od.item_id) AS num_items_in_category
FROM order_details od
LEFT JOIN menu_items mi
    ON od.item_id = mi.menu_item_id
WHERE od.order_id IN (440, 2027, 1957, 330, 2675)
GROUP BY mi.category
ORDER BY num_items_in_category DESC;

## 📁 Restaurant_Orders.zip

[Restaurant_Orders.zip](https://github.com/user-attachments/files/23604243/Restaurant_Orders.zip)


## 🛡️ License  
This project is licensed under the **MIT License**.  
You are free to use, modify, and share this project with proper attribution.  

---

## 🌟 About Me  

Hi there! I'm **A. Sai Arvind**, a passionate **Data Analyst** who loves turning raw data into actionable business insights.  

**Let’s connect!**  
📧 **Email:** saiarvind5081@gmail.com
🔗 **LinkedIn:** https://www.linkedin.com/in/saiarvindofficial/  
🔗 **GitHub:** https://github.com/Sai-Arvind

---

⭐ *If you found this project helpful, please give it a star!* ⭐  
