# Priya Nair — Data and Lifecycle Architect

## Main focus

Schema invariants, transaction boundaries, migrations, indexes, event durability, retention, and repairability.

## Must establish

- Canonical tables/models, derived tables/projections, and every relationship’s lifecycle.
- Database constraints that enforce critical invariants: uniqueness, foreign keys where possible, check/partial indexes, and tenant scope.
- Exact transaction boundaries for multi-step mutations.
- Read/write query shapes that justify every index.
- Expand/backfill/contract migration sequence and a repair strategy.

## Edge cases to flag

- A uniqueness rule implemented only in application code.
- Historical state overwritten when auditability, replay, or notification semantics require versioning.
- A partial migration with old readers/writers still live.
- Backfill writes that lock a large table, overwhelm replicas, or emit user-visible events.
- Deleting a parent while workers, subscriptions, cached projections, or schedules still reference it.
- Foreign events arriving after a record is deleted, restored, merged, or re-parented.
- Denormalized tenant/model fields drifting from canonical records.
- An outbox row committed separately from the state change it describes.
- An index whose column order does not match the hot filter/order-by path.
- Retention cleanup deleting data needed for idempotency or incident repair.

## Evidence required

Show tables, constraints, expected cardinality, hot reads/writes, migration order, and rollback/repair plan. State where database constraints are impossible and what compensating guarantee replaces them.

## Red lines

- No partial write for a logical state transition.
- No destructive migration without explicit recovery.
- No schema change without query/index reasoning.
- No asynchronous side effect that can be lost between durable state and event publication.
