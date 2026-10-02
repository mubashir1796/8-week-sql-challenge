# Danny's Diner - SQL Case Study

## Overview

This project is part of Danny Ma's 8 Week SQL Challenge. The case study focuses on Danny's Diner, a small restaurant that wants to better understand its customers, sales, and membership program.

The analysis uses SQL to answer 10 business questions about customer spending, visit patterns, menu preferences, membership activity, and loyalty points.

## Business Questions

The analysis answers the following questions:

1. How much money did each customer spend?
2. How many days did each customer visit the restaurant?
3. What was the first item purchased by each customer?
4. What is the most purchased item on the menu?
5. What is the most popular item for each customer?
6. Which item was purchased first after each customer became a member?
7. Which item was purchased just before each customer became a member?
8. How many items did each member purchase, and how much did they spend before becoming a member?
9. How many loyalty points did each customer earn?
10. How many points did customers A and B have at the end of January under the membership points rules?

## Dataset

The case study contains three tables:

* `sales` — customer purchases, including customer ID, order date, and product ID
* `menu` — menu items and their prices
* `members` — customer membership information and join dates

### Database Structure

```text
sales
├── customer_id
├── order_date
└── product_id

menu
├── product_id
├── product_name
└── price

members
├── customer_id
└── join_date
```

## SQL Skills Used

This project uses several core SQL concepts:

* `SELECT`
* `WHERE`
* `JOIN`
* `GROUP BY`
* `ORDER BY`
* `COUNT()`
* `COUNT(DISTINCT)`
* `SUM()`
* `MIN()`
* `MAX()`
* `DISTINCT`
* Subqueries
* `CASE WHEN`
* Date filtering
* Date intervals

## Analysis Approach

The analysis combines the three tables to connect customer purchases with menu information and membership dates.

For example, the `sales` table records which product a customer purchased, while the `menu` table provides the product name and price. The `members` table is then used when the analysis needs to compare purchases with a customer's membership date.

The queries were written to answer each business question separately and are stored in `dannys_diner.sql`.

## Key Findings

Some of the main results from the analysis include:

* Customer A spent **$76** in total.
* Customer B spent **$74** in total.
* Customer C spent **$36** in total.
* Customer A visited on **4 different days**.
* Customer B visited on **6 different days**.
* Customer C visited on **2 different days**.
* Ramen was the most purchased menu item overall, with **8 purchases**.
* Customer A's first purchase was sushi.
* Customer B's first purchase was curry.
* Customer C's first purchase was ramen.

The analysis also examined purchases before and after membership and calculated loyalty points using the program's different point multipliers.

## Files

| File               | Description                                                     |
| ------------------ | --------------------------------------------------------------- |
| `README.md`        | Project overview, business questions, SQL methods, and findings |
| `dannys_diner.sql` | SQL queries used to answer all 10 case study questions          |

## Tools

* SQL
* PostgreSQL
* GitHub

## Source

This case study is from Danny Ma's **8 Week SQL Challenge**.

The project is an independent practice and portfolio project created to develop SQL and data analysis skills.
