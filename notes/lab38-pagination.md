# Lab 38 — Compare Offset and Keyset Paging

## Offset Cost

Offset paging uses OFFSET and LIMIT to skip a specified number of rows before returning results. As the offset grows, the database must read and discard more rows before reaching the desired page, which can increase query cost and response time.

Example:

SELECT *
FROM orders
ORDER BY id
LIMIT 20 OFFSET 1000;

In this example, the database skips the first 1,000 rows before returning the next 20 rows.

## Keyset Query

Keyset paging retrieves rows based on the last value from the previous page rather than skipping rows. This approach is often more efficient because it allows the database to continue from a known position in the index.

Example:

SELECT *
FROM orders
WHERE id > 1000
ORDER BY id
LIMIT 20;

The query starts after the last retrieved ID and returns the next set of rows.

## Trade-off

Offset paging is simple to implement and supports direct page navigation, such as jumping to page 50. However, performance can decrease as offsets become larger.

Keyset paging generally provides better performance for large datasets because it avoids scanning and
