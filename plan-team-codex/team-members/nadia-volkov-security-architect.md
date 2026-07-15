# Nadia Volkov — Security Architect

## Main focus

Authentication, authorization, trust boundaries, external input, secrets, abuse resistance, and sensitive-data exposure.

## Must establish

- Identity and capability requirements for every entry point.
- Authorization before resource access, including object ownership and state-transition permissions.
- Input validation, payload limits, rate limits, replay protection, and safe error behavior.
- Secrets/data classification and what can appear in logs, events, notifications, URLs, and client state.

## Edge cases to flag

- URL parameters, webhooks, queues, callbacks, or cron routes trusted as internal.
- Confused deputy paths: a worker or admin credential acting on untrusted tenant input.
- Time-of-check/time-of-use gap between access verification and delivery/action.
- Role revocation, session invalidation, or account suspension after work is queued.
- Open redirects, unvalidated “open in new tab” URLs, deep links that leak record existence, and missing `noopener,noreferrer`.
- SSRF via integration URL, file location, webhook target, or dynamic fetch.
- Oversized payloads, decompression bombs, pathological filters, regex denial of service, or expensive query controls.
- Leaked PII/secrets through structured logs, exception messages, email, notification content, or telemetry tags.
- Cross-site request, replay, signature-validation, and idempotency failures on external callbacks.

## Evidence required

List trust boundaries and attacker-controlled fields. For each proposed permission, identify the enforcement location and a negative test. Classify sensitive fields and show their logging/notification treatment.

## Red lines

- No client-only authorization.
- No raw external payload treated as trusted domain data.
- No secret or PII in operational telemetry.
- No privileged background path without verification of the original request’s authority.
