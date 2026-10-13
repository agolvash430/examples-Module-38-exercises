# Lab 38 — Read an Execution Plan

## EXPLAIN vs ANALYZE

EXPLAIN shows the execution plan that the database optimizer expects to use for a query. It displays estimated costs, row counts, and operations without running the query. ANALYZE executes the query and reports the actual execution statistics, allowing comparison between estimated and actual performance.

Example:

EXPLAIN
SELECT *
FROM orders
WHERE customer_id = 100;

EXPLAIN ANALYZE
SELECT *
FROM orders
WHERE customer_id = 100;

EXPLAIN is useful for understanding planned behavior, while ANALYZE is useful for verifying real-world performance.

## Scan Types

Execution plans often include different scan types depending on how data is accessed.

Common scan types include:

- Sequential Scan: Reads all rows in a table.
- Index Scan: Uses an index to locate rows.
- Index Only Scan: Retrieves data directly from an index without reading the table.
- Bitmap Index Scan: Uses a bitmap of matching rows before accessing table data.

In general, index-based scans are preferred when they reduce the number of rows that must be read.

## Estimate Gap

An estimate gap occurs when the optimizer's estimated row count differs significantly from the actual row count reported by ANALYZE. Large estimate gaps can indicate outdated statistics, uneven data distribution, or suboptimal query plans.

Example:

Estimated Rows: 100
Actual Rows: 10,000

When estimate gaps are large, the optimizer may choose inefficient operations because it has an inaccurate understanding of the data.

## Read Order

Execution plans are typically read from the bottom upward. Lower operations execute first and provide data to higher operations. The top node represents the final result returned to the user.

Example:

Aggregate
 └─ Index Scan
     └─ Table Access

In this plan, the table access occurs first, the index scan processes the rows, and the aggregate operation produces the final result.

Understanding read order helps identify where most of the work is occurring in a query.

## Scope

Pre-lab only. This exercise focuses on understanding the differences between EXPLAIN and ANALYZE, recognizing common scan types, identifying estimate gaps, and reading execution plans in the correct order. Do not complete the full lab or perform detailed query optimization in this exercise.
