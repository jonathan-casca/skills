# AI And Agent Readiness Prompts

```text
Audit this product for AI feature readiness. Identify every place model output affects users, data, decisions, workflows, external calls, or stored records. For each, define validation, human review, confidence thresholds, audit logs, rollback, evals, and abuse cases.
```

```text
Review all LLM prompts and agent workflows for production safety. Look for prompt injection, tool abuse, data exfiltration, hallucinated actions, unsafe autonomy, missing guardrails, weak system prompts, missing output validation, and lack of observability.
```

```text
Design an eval framework for this AI feature. Include golden datasets, adversarial cases, regression tests, scoring rubrics, human review, CI gates, production monitoring, drift detection, and a process for changing prompts safely.
```

```text
Create a cost-control plan for AI usage. Include per-tenant limits, per-user limits, token budgets, queueing, caching, model selection, retries, timeout caps, abuse detection, dashboards, alerts, and graceful degradation when budgets are hit.
```

```text
Audit AI-generated content storage and display. Check provenance, user visibility, edit history, confidence display, source citations, hallucination risk, PII handling, retention, deletion, and dispute/correction workflows.
```

```text
Review agent tool permissions. For every tool an agent can call, classify it as read-only, write, destructive, external side effect, or sensitive data access. Propose permission boundaries, confirmations, dry-run mode, audit logs, and test cases.
```
