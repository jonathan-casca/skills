# Team Member Selection

Every team member has a separate, substantive brief in [`team-members/`](team-members/). Select only people who expose a real risk in the task; no generic “advisors,” duplicate roles, or fictional biography.

| Team member | Primary risk owned | Select when |
|---|---|---|
| [Ada Chen — Systems](team-members/ada-chen-systems-architect.md) | Duplicate authority, bad boundaries, unrecoverable derived state | Always |
| [Iris Gomez — Reuse](team-members/iris-gomez-reuse-architect.md) | Rebuilding existing capability or unsafe copy-and-rename reuse | Large/legacy codebases, shared features, refactors, new platform primitives |
| [Marcus Reed — Domain/API](team-members/marcus-reed-domain-api-architect.md) | Invalid command/query contracts and ownership gaps | New APIs, domain flows, UI-backed mutations |
| [Priya Nair — Data/Lifecycle](team-members/priya-nair-data-lifecycle-architect.md) | Data corruption, migration, index, event-durability failures | Schema, consistency, migrations, history, workers |
| [Elena Kovacs — Runtime/Scale](team-members/elena-kovacs-runtime-scale-architect.md) | Redis, queue, cache, fan-out, throughput, and backpressure failure | Queues, Redis, jobs, notifications, caching, scale |
| [Omar Hassan — Multi-Tenancy](team-members/omar-hassan-multi-tenancy-architect.md) | Cross-tenant reads, writes, cache/queue leakage | Any tenant data, role/grant, or organization scope |
| [Nadia Volkov — Security](team-members/nadia-volkov-security-architect.md) | Capability escalation, unsafe input, secret/PII exposure | Auth, sensitive data, webhooks, external input, deep links |
| [Caleb Ward — Reliability](team-members/caleb-ward-reliability-architect.md) | Dependency, rollout, observability, and incident-recovery gaps | Multi-service, async, high-criticality, operational changes |
| [Sofia Ibarra — Integrations](team-members/sofia-ibarra-integration-architect.md) | Vendor contract, webhook, import/export, replay, and reconciliation failures | External APIs, identity providers, webhooks, data import/export |
| [Maya Patel — Delivery/Verification](team-members/maya-patel-delivery-verification-architect.md) | Risk-last execution, missing proof, weak test or rollout plan | Always |

## Selection Rules

- Always select Ada and Maya.
- Add Iris for a large codebase, an existing subsystem being extended, refactoring, or any proposal for a new shared primitive. In this repository, default to selecting Iris unless the task is an isolated one-file change.
- Add Marcus for any new endpoint, UI flow, state transition, or shared domain capability.
- Add Priya for persistence, data history, migrations, projections, transactions, or durable events.
- Add Elena whenever background work, queues, Redis, caches, scheduled tasks, notifications, rate limits, or scale are involved.
- Add Omar whenever records belong to organizations/tenants or roles/grants can affect access.
- Add Nadia for authentication, authorization, user data, external input, secrets, callbacks, or deep links.
- Add Caleb for external dependencies, worker pipelines, production reliability, observability, or deployment changes.
- Add Sofia only when another system’s contract or imported/exported data is part of the architecture.
- `best`: 4–6 members; `lite` and `single`: 3–5. If the task needs more, split it into focused planning runs rather than assembling a crowd.
