# Big Sweep Prompts

```text
Run a full platform-hardening sweep on this repository. Phase 1: map the app architecture, data model, auth model, API surface, background jobs, integrations, and deployment path. Phase 2: identify production-readiness gaps across security, data integrity, reliability, observability, performance, privacy, testing, and support tooling. Phase 3: rank the top 15 issues by customer impact and implementation effort. Phase 4: implement the highest-impact low-risk fixes first, with focused tests and minimal unrelated refactors.
```

```text
Act as a staff engineer preparing this product for enterprise customers. Review the repository for tenant isolation, audit logs, admin permissions, compliance evidence, SSO readiness, data retention, exportability, observability, support workflows, incident response, and upgrade safety. Produce an enterprise-readiness gap list and then implement the most urgent safe fixes.
```

```text
Pretend you inherited this app after a prototype phase and must make it maintainable for a team of engineers. First, identify the core domains and module boundaries. Then find the largest sources of coupling, duplicated business rules, weak types, and untested workflows. Create a refactor plan that preserves behavior, then execute the first small refactor with tests.
```

```text
Take this codebase from demo to production. Do not focus on cosmetic polish. Focus on the boring systems work: auth, ownership checks, bounded queries, transactions, idempotency, structured logs, retry caps, dead letters, alerting, support tools, migrations, env validation, and critical tests. Work in small commits or clearly separated patches.
```

```text
Run a red-team style production readiness review. Try to break this app as a malicious user, a confused customer, a large tenant, a flaky third-party provider, a failed deploy, a duplicate webhook, a slow database, and a support engineer under pressure. For each persona, list the breakpoints and the smallest durable fix.
```

```text
Create a 30/60/90 day platform roadmap for this product. The first 30 days should remove launch blockers and security/data risks. The next 30 should improve reliability, observability, and supportability. The final 30 should improve scalability, developer velocity, and compliance posture. Include concrete engineering tasks, owners, and acceptance criteria.
```

```text
Build a production-readiness scorecard for this repository. Score each category from 1 to 5: authentication, authorization, data model, migrations, API contracts, integrations, background jobs, observability, incident response, security, privacy, testing, CI/CD, admin tooling, frontend resilience, performance, and maintainability. Justify each score with evidence from the codebase and recommend the next 10 fixes.
```

```text
Work like an autonomous platform engineer for one day on this codebase. Start with discovery, write down the highest-risk platform gaps, pick the best fix that is small enough to complete safely, implement it, add tests, run targeted validation, and leave a concise handoff note with remaining risks.
```

```text
Run a founder-to-platform transition review. Assume the product was built fast by a small team and now needs to support real customers. Identify what must change in engineering practices, code architecture, deployment, support, monitoring, security, billing, data governance, and product operations. Convert the review into a prioritized execution backlog.
```

```text
Review this application for silent failure risks. Find places where errors are swallowed, retries hide permanent failures, UI shows success before durable writes, jobs fail without alerts, webhooks can be missed, logs lack correlation IDs, or users can get stuck without support visibility. Implement the safest high-impact fix.
```
