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

## Meta Prompt

```text
You are not here to make the demo look better. You are here to make the application survive production. Review and improve this codebase through the lens of security, data integrity, reliability, observability, supportability, and maintainability. Prioritize boring platform work over shiny product work.
```
