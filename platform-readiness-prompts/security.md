# Security Prompts

```text
Perform a security review of this codebase. Focus on auth, authorization, input validation, injection, file uploads, webhooks, secrets, PII handling, SSRF, CSRF, rate limiting, and dependency risks.
```

```text
Find every place user input crosses a trust boundary. Verify validation, sanitization, authorization, and safe error handling. Return risky locations and fixes.
```

```text
Audit all file upload/download flows. Check MIME validation, size limits, malware risk, access control, signed URLs, storage permissions, and filename/path safety.
```

```text
Review webhook handlers for signature verification, replay protection, idempotency, logging, retries, and failure behavior.
```

```text
Search this codebase for secrets, tokens, API keys, unsafe env var usage, and places secrets might be logged or exposed to the client.
```
