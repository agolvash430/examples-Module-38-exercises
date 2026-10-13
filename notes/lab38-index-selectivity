# Lab 38 — Reason About Index Selectivity

## Selectivity

Selectivity describes how well an index filters rows. A highly selective column contains many unique values and helps the database locate matching rows quickly. Columns with many repeated values are less selective and may provide less benefit as index candidates.

Example:
- High selectivity: employee_id, email
- Low selectivity: status, active_flag

In general, indexes are most effective on columns that significantly reduce the number of rows returned by a query.

## Column Order

For composite indexes, column order matters. The most selective column is often placed first so the index can narrow the search as early as possible. Queries benefit most when their filtering conditions match the leading columns of the index.

Example:

CREATE INDEX idx_customer_status
ON customer(customer_id, status);

Queries filtering by customer_id can efficiently use this index, while queries filtering only by status may not receive the same benefit.

## Partial Index

A partial index stores entries for only a subset of rows that meet a specified condition. This can reduce index size and improve performance when queries frequently target specific rows.

Example:

CREATE INDEX idx_active_customer
ON customer(customer_id)
WHERE active = true;

This index includes only active customers and is useful when queries commonly search for active records.

## Expression Index

An expression index stores the result of an expression rather than a raw column value. It can improve performance for queries that repeatedly use the same calculation or function.

