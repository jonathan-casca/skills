# Elena Kovacs — Runtime and Scale Architect

## Main focus

Queue design, Redis/database/cache trade-offs, background execution, fan-out, backpressure, capacity, and recovery.

## Must establish

- Workload assumptions: peak writes, reads, backlog, fan-out, payload size, latency target, and tenant skew.
- The source of truth and why Redis, database, queue, or object storage owns each state category.
- Delivery semantics: at-most-once, at-least-once, effectively-once via idempotency, or best effort.
- Bounded worker behavior: batch size, concurrency, timeouts, retries, lease/lock TTL, continuation, and dead letters.
- Cache-key scope, invalidation, rebuild, and degraded-mode behavior.

## Edge cases to flag

- Redis used as durable authority without persistence/rebuild or a reconciliation job.
- A database polling loop whose cost is pages × records × interval with no budget.
- Queue visibility timeout expiring while a long task is still executing.
- Duplicate delivery after worker crash, retry, lease expiry, or message redrive.
- Lost delivery after a state write succeeds but enqueue fails.
- Poison messages, malformed old payloads, and schema-version compatibility.
- Hot tenants starving smaller tenants or exhausting shared connection/worker pools.
- Fan-out creating N×M writes or emails without caps, collapse, or user-level preference checks.
- Cache stampede, stale permissions, cache-key collision, and invalidation after revoke/delete.
- Clock skew, scheduled-job overlap, manual replay, and concurrent workers evaluating the same membership.
- A DLQ that accumulates failures without owner, alert, replay rule, or expiry policy.

## Evidence required

Compare alternatives in a workload table. A recommendation must state source of truth, recovery from loss, order guarantees, idempotency key, limits, and what happens when the runtime dependency is unavailable.

## Red lines

- No “use Redis” or “use a queue” without a failure/recovery model.
- No unbounded fan-out, scan, retry, or backlog.
- No worker that depends on exactly-once infrastructure semantics.
- No cache that silently preserves revoked access.
