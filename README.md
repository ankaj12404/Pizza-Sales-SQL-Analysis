# Pizza-Sales-SQL-Analysis
# 🍕 Pizza Sales Data Analysis Using SQL

This project analyzes a pizza sales dataset using MySQL to extract business insights from transactional data.

## 📊 Project Objective

To perform structured query analysis using:

- Joins
- Group By
- Order By
- Having
- Where
- Aggregate Functions

The goal is to transform raw order data into meaningful business insights.

---

## 🗂️ Database Structure

Tables used:

1. orders
2. order_details
3. pizzas

---

## 🔎 Business Questions Solved

### 1️⃣ Total Revenue Generated

```sql
SELECT ROUND(SUM(order_details.quantity * pizzas.price), 2) AS total_sales
FROM order_details
JOIN pizzas
ON pizzas.pizza_id = order_details.pizza_id;

2️⃣ Most Common Pizza Size Ordered
SELECT pizzas.size,
COUNT(order_details.order_details_id) AS total_orders
FROM pizzas
JOIN order_details
ON pizzas.pizza_id = order_details.pizza_id
GROUP BY pizzas.size
ORDER BY total_orders DESC;

3️⃣ Orders Placed by Weekday
SELECT DAYNAME(orders.date) AS day_name,
COUNT(orders.order_id) AS total_orders
FROM orders
GROUP BY DAYNAME(orders.date)
ORDER BY total_orders DESC;

4️⃣ Hourly Comparison of Large vs Small Pizzas
SELECT HOUR(orders.time) AS order_hour,
SUM(CASE WHEN pizzas.size = 'L' THEN order_details.quantity ELSE 0 END) AS total_large_pizzas,
SUM(CASE WHEN pizzas.size = 'S' THEN order_details.quantity ELSE 0 END) AS total_small_pizzas
FROM orders
JOIN order_details
ON orders.order_id = order_details.order_id
JOIN pizzas
ON order_details.pizza_id = pizzas.pizza_id
GROUP BY HOUR(orders.time)
HAVING total_large_pizzas > total_small_pizzas
ORDER BY order_hour;

5️⃣ Highest Priced Pizza
SELECT pizza_id, price
FROM pizzas
ORDER BY price DESC
LIMIT 1;

