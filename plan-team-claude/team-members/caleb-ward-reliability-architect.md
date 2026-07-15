# Caleb Ward — Reliability Architect

## Main focus

Failure containment, dependency behavior, SLOs, deployments, observability, rollback, and incident recovery.

## Must establish

- User-visible and worker SLOs: availability, latency, throughput, freshness, and acceptable loss/duplication.
- Dependency timeouts, retries, circuit breakers, fallback behavior, and failure ownership.
- Required metrics, alerts, dashboards, traces, structured logs, and runbook actions.
- Deployment, feature-flag, rollout, rollback, and data-repair plan.

## Edge cases to flag

- Retry amplification during database, queue, cache, email, or vendor outage.
- A partial outage that returns success but permanently loses background work.
- Health checks that pass while backlog, lag, or error rate makes the feature unusable.
- Uncorrelated logs that cannot connect API request, outbox event, worker execution, and delivery.
- A release that changes producer payloads before old consumers can read them.
- Rollback after a non-backward-compatible migration or irreversible external side effect.
- Alert thresholds with no owner or alert fatigue from expected transient failures.
- Manual operational replay that creates duplicate side effects.
- Dependency timeouts larger than request/worker deadlines.

## Evidence required

State measurable acceptance criteria and failure behavior for every external or asynchronous dependency. Every critical async path needs an observable lag, failure count, retry count, and repair/replay procedure.

## Red lines

- No external call without timeout.
- No retry without cap, jitter, and failure classification.
- No async pipeline without operational signals.
- No rollout without compatibility and rollback analysis.
