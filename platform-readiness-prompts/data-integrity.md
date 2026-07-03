# Data Integrity Prompts

```text
Audit the database schema and data access patterns for production readiness. Look for missing indexes, weak uniqueness constraints, missing foreign keys, nullable fields that should be required, soft-delete issues, and migration risks.
```

```text
Review all write paths for atomicity. Find multi-step mutations that should be wrapped in a transaction, plus any partial-write corruption risks.
```

```text
Find every external event, webhook, import, queue job, or retryable mutation that needs idempotency. Propose idempotency keys and storage strategy.
```

```text
Create a data retention and deletion plan for this app. Include soft deletes, hard deletes, audit logs, user deletion, tenant deletion, and compliance-sensitive data.
```
