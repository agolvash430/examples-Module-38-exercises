# Lab 38 — Fix Sargability and N+1

## Sargable Rewrite

A query is sargable when the database can efficiently use an index to locate rows. Applying functions or calculations directly to indexed columns may prevent index usage and force a table scan.

Non-sargable example:

SELECT *
FROM customer
WHERE LOWER(email) = 'user@example.com';

Sargable example:

SELECT *
FROM customer
WHERE email = 'user@example.com';

Sargable queries generally improve performance because the optimizer can make effective use of available indexes.

## N+1 Shape

The N+1 problem occurs when an application executes one query to retrieve a list of records and then executes an additional query for each record in that list.

Example:

1 query to load customers

SELECT *
FROM customer;

N additional queries to load orders

SELECT *
FROM orders
WHERE customer_id = ?;

If 100 customers are returned, the application may execute 101 separate queries. This increases database load and response time.

## N+1 Fix

The N+1 problem can often be solved by retrieving related data in a single query using a JOIN or by batching requests.

Example:

SELECT c.id,
       c.name,
       o.id AS order_id
FROM customer c
LEFT JOIN orders o
    ON c.id = o.customer_id;

This approach reduces the number of database round trips and allows the database optimizer to perform the relationship lookup efficiently.

## SELECT * Cost

Using SELECT * retrieves every column from a table, even when many columns are not needed. This increases disk reads, memory usage, network traffic, and query processing costs.

Less efficient:

SELECT *
FROM customer;

More efficient:

SELECT id,
       name,
       email
FROM customer;

Selecting only the required columns can improve performance and reduce resource consumption.

## Scope

Pre-lab only. This exercise focuses on understanding sargable query design, recognizing the N+1 query pattern, identifying common solutions to N+1 issues, and understanding the performance costs of SELECT *. Do not complete the full lab or perform the final query optimizations in this 
