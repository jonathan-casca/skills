# Platform Readiness Prompt Pack

Copy-paste prompts for Claude, Codex, or other coding agents to turn a vibe-coded app into something closer to a production platform.

## Files

- `platform-readiness-audit.md` - broad production-readiness reviews
- `auth-authorization.md` - login, roles, ownership, and tenant isolation
- `data-integrity.md` - schema, transactions, idempotency, and retention
- `observability.md` - logs, metrics, traces, alerts, and dashboards
- `security.md` - threat review, input validation, webhooks, secrets, and files
- `reliability.md` - external calls, queues, retries, limits, and graceful failure
- `testing.md` - practical test strategy and regression coverage
- `deployment-ci.md` - CI, environment validation, releases, and rollback
- `admin-support-tooling.md` - internal tooling and customer support workflows
- `frontend-product-quality.md` - UX states, forms, accessibility, and async flows
- `architecture-maintainability.md` - module boundaries, TypeScript, and refactoring
- `go-fix-it.md` - prompts that ask the agent to implement fixes directly
- `launch-readiness.md` - launch gates, go/no-go checks, rollout planning
- `incident-response.md` - incident drills, runbooks, recovery, and postmortems
- `billing-monetization.md` - billing correctness, subscriptions, entitlements, and finance ops
- `privacy-compliance.md` - privacy, data governance, consent, retention, and access controls
- `ai-agent-readiness.md` - AI feature safety, evals, prompts, guardrails, and cost controls
- `api-contracts-integrations.md` - public APIs, SDKs, webhooks, integrations, and versioning
- `performance-scale.md` - profiling, load testing, database scale, caching, and cost
- `migration-backfill.md` - data migrations, backfills, rollouts, and rollback safety
- `product-ops.md` - feature flags, analytics, lifecycle emails, and operational workflows
- `big-sweep-prompts.md` - larger multi-phase prompts for agents to run end-to-end

## Meta Prompt

```text
You are not here to make the demo look better. You are here to make the application survive production. Review and improve this codebase through the lens of security, data integrity, reliability, observability, supportability, and maintainability. Prioritize boring platform work over shiny product work.
```
