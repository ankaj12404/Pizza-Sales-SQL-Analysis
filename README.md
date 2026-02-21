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
