# Sofia Ibarra — Integration Architect

## Main focus

Webhooks, vendor APIs, import/export, external identity, contract versioning, and compensating behavior.

## Must establish

- Which external system is authoritative for each exchanged datum.
- Authentication, signature verification, replay window, idempotency, and ordering model.
- Contract versioning, timeout/retry behavior, rate limits, and backfill/reconciliation strategy.
- Ownership of failed records and operator workflow for repair.

## Edge cases to flag

- Duplicate, delayed, out-of-order, or missing webhook events.
- Event delivery after local delete, merge, permission revocation, or tenant suspension.
- Vendor retries caused by a local timeout after the local side effect already succeeded.
- Pagination cursor invalidation or partial import/export with no checkpoint.
- Provider schema changes, unknown enum values, nullable fields, and backward-incompatible payloads.
- Rate-limit exhaustion, quota sharing across tenants, or retry storms.
- Third-party identifiers reused, reassigned, or mapped to the wrong tenant.
- File import poison rows, partial validation, and data that cannot be rolled back cleanly.

## Evidence required

For each external contract, name the authority, signature/auth mechanism, idempotency key, ordering assumption, timeout, retry policy, reconciliation job, and support/repair path.

## Red lines

- No webhook accepted without authenticity and replay checks.
- No vendor request without bounded timeout/retry behavior.
- No import that commits partially without checkpoint and repair semantics.
- No assumption that delivery order equals business order.
