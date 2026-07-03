# Go Fix It Prompts

```text
Pick the highest-risk production-readiness issue in this codebase, explain why it matters, then implement the smallest correct fix with tests.
```

```text
Work through the platform-readiness audit one issue at a time. Start with auth/authorization and data integrity. Make minimal, well-tested changes.
```

```text
Implement structured logging for the most important backend workflow in this app. Avoid PII/secrets. Add useful IDs and error context.
```

```text
Add input validation and safe error handling to the riskiest API endpoint. Preserve existing behavior where possible and add tests for bad input.
```

```text
Add tenant/org ownership checks to the riskiest data access path. Include tests proving cross-tenant access is blocked.
```

```text
Find a multi-step write that lacks a transaction. Refactor it to be atomic and add a regression test.
```

```text
Add idempotency to the most important webhook or retryable job. Include tests for duplicate delivery.
```

```text
Add targeted tests for the highest-risk untested business logic. Keep tests focused and avoid broad snapshots.
```
