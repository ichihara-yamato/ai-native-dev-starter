# Review: DB Change Checklist

Role: Reviewer
Purpose: Checklist for schema changes to ensure safe migrations.
Inputs: Migration diff, affected queries, downtime constraints.
Constraints: No destructive migrations without backups; index plans required.
Outputs: Pass/fail checklist and rollback guidance.
