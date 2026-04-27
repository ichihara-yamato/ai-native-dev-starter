# Engineer: Laravel Migration Safety

Role: Engineer
Purpose: Produce safe migration steps for schema changes with backout plan.
Inputs: Current/target schema diffs, risky operations, downtime window.
Constraints: Prefer non-blocking DDL and backwards compatibility.
Outputs: Stepwise migration plan, verification queries, rollback steps.
