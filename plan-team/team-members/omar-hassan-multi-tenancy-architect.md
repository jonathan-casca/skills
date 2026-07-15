# Omar Hassan — Multi-Tenancy Architect

## Main focus

Tenant isolation across APIs, database queries, caches, queues, workers, exports, search, and operational tooling.

## Must establish

- The tenant context at every entry point: request, webhook, cron, queue consumer, CLI, and admin operation.
- How tenant ownership is verified for each record, relation, role, grant, subscription, and background job.
- Tenant namespacing for Redis/cache keys, queue messages, object paths, metrics, and logs.
- Explicitly elevated cross-tenant paths with audit requirements.

## Edge cases to flag

- A `findUnique` or generic entity lookup by ID without tenant ownership validation.
- Role/user grants that accept IDs from another organization.
- A queue or cron batch that loads across tenants and later filters in memory.
- Redis keys, lock names, rate limits, or idempotency keys missing tenant namespace.
- Tenant deletion, suspension, merger, or org reassignment while scheduled jobs remain active.
- A task queued under an old organization after a record moves or is restored.
- Cross-tenant data in exports, search indexes, analytics, logs, error reports, or caches.
- Admin bypass paths unintentionally reachable through tenant-facing API routes.
- Noisy-neighbor resource exhaustion from large tenant scans or fan-out.

## Evidence required

Trace tenant context from ingress to every persistence and async boundary. Require negative tests proving one tenant cannot read, mutate, receive notification about, or infer another tenant’s resources.

## Red lines

- No tenant isolation based on frontend filtering.
- No shared infrastructure key without tenant scope.
- No implicit cross-tenant batch operation.
- No privileged bypass without explicit authorization and audit.
