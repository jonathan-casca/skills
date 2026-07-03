# Launch Readiness Prompts

```text
Run a launch readiness review for this application. Treat the launch as real, with paying customers, production data, support burden, and rollback risk. Produce a go/no-go report with: critical blockers, high-priority risks, acceptable risks, owners, verification steps, and the smallest set of changes required before launch.
```

```text
Create a production launch checklist for this repo. Include security, auth, billing, data integrity, migrations, observability, alerts, on-call, support tooling, backups, disaster recovery, legal/compliance, analytics, feature flags, and customer communication. Mark each item as must-have, should-have, or can-wait.
```

```text
Design a staged rollout plan for this app. Include internal dogfood, beta customers, limited percentage rollout, feature flags, kill switches, metrics to watch, rollback criteria, support escalation, and the exact signals that mean the rollout should pause.
```

```text
Pretend you are the launch approver. Review the codebase and write the launch approval memo you would send to leadership. Be blunt about what is not ready. Include the top 10 launch risks, why each matters, how to detect it, and what mitigation is required.
```

```text
Create a launch smoke test plan that can be run after every deploy. Include login, critical user flows, data writes, background jobs, email/webhook delivery, billing if applicable, admin/support workflows, and observability checks.
```

```text
Review this app for missing kill switches and operational controls. Identify high-risk features that need feature flags, rate limits, admin disable switches, provider failover controls, or per-tenant rollout controls before launch.
```
