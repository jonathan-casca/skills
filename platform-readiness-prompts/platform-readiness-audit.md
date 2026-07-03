# Platform Readiness Audit Prompts

```text
Review this codebase like a senior platform engineer. Identify the top missing pieces that would prevent this from being production-ready: auth, authorization, observability, data integrity, background jobs, security, testing, deployment, and support tooling. Prioritize findings by risk and give concrete implementation tasks.
```

```text
Audit this app for demo code that will fail under real users. Look for fragile assumptions, missing error handling, unbounded queries, hardcoded values, missing indexes, no retries, weak validation, and poor module boundaries. Return a prioritized fix list.
```

```text
Create a platform-readiness checklist for this repository. For each category, mark: already present, partially present, missing, and risky. Include specific files/modules to inspect or change.
```

```text
Pretend this app is launching to 100 paying customers next month. What must be built before launch? Focus on security, reliability, supportability, deployment, data safety, and operational visibility.
```
