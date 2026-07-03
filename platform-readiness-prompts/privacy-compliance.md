# Privacy And Compliance Prompts

```text
Perform a privacy and data governance review for this app. Identify personal data, sensitive data, secrets, customer data, generated content, logs, analytics payloads, third-party sharing, retention requirements, deletion flows, export flows, and consent requirements.
```

```text
Create a data inventory for this codebase. Map every major data type to where it is collected, stored, processed, logged, exported, shared with vendors, retained, deleted, and accessed by admins.
```

```text
Audit this app for PII leaks. Search backend logs, frontend analytics, error reporting, URLs, local storage, emails, exports, webhooks, file names, and third-party calls. Return exact risks and fixes.
```

```text
Design user and tenant deletion workflows. Include soft delete vs hard delete, legal holds, audit log retention, backup retention, async cleanup, vendor deletion, idempotency, verification, and support/admin tooling.
```

```text
Review access controls for privacy-sensitive data. Identify who can view, export, mutate, delete, or impersonate users/tenants. Add least-privilege recommendations and audit log requirements.
```

```text
Create a compliance readiness checklist for SOC 2-style expectations. Cover access control, change management, monitoring, incident response, vendor management, audit logs, backups, encryption, secrets, and evidence collection.
```
