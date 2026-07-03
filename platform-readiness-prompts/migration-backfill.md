# Migration And Backfill Prompts

```text
Review the migration and backfill safety of this app. Identify schema changes that need expand/contract rollout, nullable transition fields, background backfills, dual writes, data verification, rollback plans, and customer-impacting risks.
```

```text
Design a safe backfill plan for a large production table. Include batching, ordering, retries, resume checkpoints, concurrency limits, transaction size, observability, dry-run mode, verification queries, and rollback strategy.
```

```text
Audit this repository for risky data migrations. Look for destructive changes, blocking migrations, rewritten columns, missing defaults, long locks, untested assumptions, and code that assumes the migration completed instantly.
```

```text
Create an expand-and-contract migration plan for changing a core data model. Include schema expansion, code compatibility, backfill, verification, traffic monitoring, cleanup migration, and rollback at each phase.
```

```text
Review all places where persisted data shape is assumed. Find missing backwards compatibility, weak parsers, unsafe JSON casts, deleted enum values, and old records that could break new code.
```

```text
Write a production data repair plan for this app. Include how to detect bad records, preview changes, apply fixes safely, audit the repair, notify affected users if needed, and prevent recurrence.
```
