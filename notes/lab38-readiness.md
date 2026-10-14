# Lab 38 — Plan the Tuning Evidence

## Workflow

A structured performance-tuning workflow begins by measuring the current query performance, identifying bottlenecks through execution plans, making a single optimization, and then measuring performance again. Comparing results before and after the change helps determine whether the optimization was effective.

Typical workflow:

1. Capture baseline performance.
2. Review the execution plan.
3. Identify a potential bottleneck.
4. Apply one tuning change.
5. Re-run the query.
6. Compare results.
7. Document findings.

Following a repeatable process helps ensure that conclusions are based on evidence rather than assumptions.

## Evidence Pair

Performance tuning should be supported by a before-and-after evidence pair. This allows objective comparison of query behavior and execution costs.

Examples of evidence:

- Before execution plan and after execution plan
- Before execution time and after execution time
- Before row counts and after row 
