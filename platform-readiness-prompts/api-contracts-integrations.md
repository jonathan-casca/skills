# API Contracts And Integrations Prompts

```text
Audit this app's API surface for production readiness. Include authentication, authorization, input schemas, response schemas, error codes, pagination, rate limits, idempotency, versioning, backwards compatibility, documentation, and observability.
```

```text
Review all integration points with third-party services. For each provider, document the contract, timeout behavior, retry behavior, failure mapping, credentials, rate limits, webhook handling, reconciliation, and local/staging test strategy.
```

```text
Design a public API strategy for this product. Include resource modeling, auth, scopes, idempotency keys, pagination, filtering, sorting, webhooks, SDKs, versioning, deprecation policy, docs, examples, and support workflows.
```

```text
Audit webhook producers and consumers. Verify signature verification, replay protection, event ordering, duplicate delivery, retry caps, dead-letter queues, event versioning, payload contracts, and observability.
```

```text
Create integration contract tests for the riskiest external service in this app. Include success, validation error, auth error, timeout, rate limit, provider outage, malformed response, duplicate webhook, and stale data cases.
```

```text
Find every API endpoint that returns lists. Verify it has pagination, maximum limits, deterministic ordering, authorization scoping, filtering validation, and tests for large data sets.
```
