# Candidate and Final Plan Contract

Every candidate decision owner and final decision owner must write a plan that stands on its own. The final plan must cite evidence packet sources and candidate plan IDs for consequential decisions.

```markdown
# [Task] — Build Plan

## Decision Summary
- **Chosen approach:**
- **Why now:**
- **Confidence:** High | Medium | Low
- **Deferred explicitly:**

## Current State and Evidence
- [Verified fact] — [path:line-range]
- [Assumption] — [validation step]

## Architecture
### Component boundaries
| Component | Owns | Does not own | Interface |

### Request and event flow
[Mermaid sequence or flow diagram when it materially clarifies the design]

### Authorization and tenancy
- Caller and procedure/service boundary:
- Resource ownership check:
- Data exposure and audit requirements:

## API Structure
| Surface | Operation | Input | Output | Auth | Error behavior |

Define:
- route/router and service responsibilities;
- validation and ownership checks;
- pagination, limits, timeouts, and idempotency;
- backward compatibility and deprecation behavior.

## Data Model and Lifecycle
### Schema changes
| Model/table | Fields and constraints | Indexes | Lifecycle |

### Consistency and migrations
- transaction boundaries:
- uniqueness/idempotency keys:
- migration expand/backfill/contract steps:
- rollback or repair strategy:

## Runtime, Queue, Redis, and Cache Analysis
Required whenever the task touches asynchronous work, state tracking, notifications,
queues, Redis, caches, or scalability.

| Concern | Workload and SLO | Source of truth | Options compared | Chosen design | Failure and recovery |

Address:
- expected read/write/fan-out volume and a stated capacity assumption;
- strong/eventual consistency needs;
- database vs Redis vs queue responsibilities;
- cache invalidation, replay, and loss/rebuild behavior;
- bounded batch size, concurrency, timeouts, retry caps, and dead-letter handling;
- idempotency and duplicate delivery;
- metrics, alerts, and operational owner.

## Delivery Plan
1. **Phase:** [vertical slice]
   - Files/systems:
   - Acceptance criteria:
   - Tests:
   - Rollback:

Order phases by risk, not by UI convenience. Front-load the least-known technical
constraint.

## Verification Strategy
- Unit:
- Integration:
- End-to-end:
- Load/failure:
- Security/tenant isolation:
- Migration:

## Observability and Operations
- Structured logs:
- Metrics and dashboards:
- Alerts:
- Runbook:

## Risks, Dissent, and Decisions Deferred
| Item | Decision | Reason | Mitigation or validation trigger |

## Decision Ledger
| Final decision | Evidence | Candidate source(s) | Rejected alternative |
```

## Quality Gates

Reject a plan as incomplete when it:

- claims a repository fact without evidence;
- says “use Redis,” “use a queue,” “make it scalable,” or “add a worker” without the runtime analysis;
- introduces a multi-step write without a transaction or explicit compensating action;
- exposes an API without authentication, authorization, and ownership behavior;
- uses an unbounded query, loop, retry, external request, or fan-out;
- creates a schema change without indexes and migration safety;
- gives only a file list instead of interfaces, data flow, and acceptance criteria;
- reaches consensus by vote instead of resolving the factual trade-off.
