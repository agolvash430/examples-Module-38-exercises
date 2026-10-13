# Lab 38 — Write the Reporting Queries

## Inner vs Left

An INNER JOIN returns only rows that have matching values in both tables. A LEFT JOIN returns all rows from the left table and any matching rows from the right table. If no match exists, the right-side columns are returned as NULL.

Example:

SELECT c.name, o.id
FROM customer c
INNER JOIN orders o
    ON c.id = o.customer_id;

SELECT c.name, o.id
FROM customer c
LEFT JOIN orders o
    ON c.id = o.customer_id;

## Aggregate

Aggregate functions summarize multiple rows into a single result. Common aggregate functions include COUNT(), SUM(), AVG(), MIN(), and MAX().

Example:

SELECT
    COUNT(*) AS total_orders,
    SUM(amount) AS total_sales,
    AVG(amount) AS average_sale,
    MIN(amount) AS smallest_sale,
    MAX(amount) AS largest_sale
FROM orders;

Aggregate functions are frequently used with GROUP BY when creating reports.

## HAVING

The HAVING clause filters grouped results after aggregation occurs. WHERE filters rows before grouping, while HAVING filters groups after grouping.

Example:

SELECT customer_id,
       COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 5;

This query returns only customers who have more than five orders.

## CTE

A Common Table Expression (CTE) is a temporary named result set created with the WITH keyword. CTEs improve readability and make complex queries easier to understand.

Example:

WITH customer_totals AS (
    SELECT customer_id,
           SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM customer_totals
WHERE total_spent > 1000;

The CTE calculates total spending for each customer and then filters the results in the main query.

## Scope

Pre-lab only. This exercise reviews the concepts needed for reporting queries, including INNER JOIN vs LEFT JOIN, aggregate functions, HAVING clauses, and Common Table Expressions (CTEs). Do not complete the full lab or write the final reporting queries in this exercise.
