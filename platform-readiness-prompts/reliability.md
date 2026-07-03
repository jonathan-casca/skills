# Reliability Prompts

```text
Review all external API calls. Add recommendations for timeouts, retries, circuit breakers, backoff, provider error mapping, observability, and fallback behavior.
```

```text
Audit background jobs and queues for production reliability. Check retry caps, dead-letter handling, idempotency, concurrency limits, logging, and stuck job recovery.
```

```text
Find all unbounded loops, unbounded queries, unbounded retries, and operations that could blow up with large customer data.
```

```text
Design graceful failure behavior for this app. For each critical workflow, define what happens when the database, queue, email provider, storage provider, or external API fails.
```
