# Incident Response Prompts

```text
Create an incident response plan for this application. Cover severity levels, alert routing, triage steps, owner responsibilities, customer communication, rollback, data repair, postmortems, and how to decide whether an incident is security-related.
```

```text
Review this codebase and identify the incidents it is most likely to have in production. For each likely incident, describe symptoms, detection signals, dashboards/logs needed, immediate mitigation, long-term fix, and customer impact.
```

```text
Write runbooks for the top 5 operational failures in this app. Include exact investigation steps, commands or dashboards to check, safe mitigations, unsafe actions to avoid, escalation criteria, and post-incident cleanup.
```

```text
Perform a game day planning exercise for this product. Simulate failures in the database, queue, auth provider, payment provider, file storage, email provider, and a critical third-party API. For each scenario, state how the app should degrade and what the operator should do.
```

```text
Audit the app for recovery gaps. Find workflows where a failed job, partial write, bad deploy, provider outage, or corrupted state would require manual database edits. Propose safe repair tools and recovery paths.
```

```text
Create a postmortem template tailored to this application. Include timeline, customer impact, detection gap, root cause, contributing factors, what went well, what went poorly, corrective actions, owners, due dates, and follow-up verification.
```
