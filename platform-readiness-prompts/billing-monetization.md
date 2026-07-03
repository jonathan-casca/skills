# Billing And Monetization Prompts

```text
Audit this app for billing readiness. Look for subscription lifecycle handling, plan changes, trials, cancellations, failed payments, invoices, refunds, taxes, entitlements, usage limits, proration, admin overrides, and audit logs. Return production blockers and concrete implementation tasks.
```

```text
Design an entitlement system for this product. Include plans, features, limits, per-tenant overrides, trial access, expired subscriptions, grace periods, backend enforcement, frontend display, audit logs, and tests for every boundary.
```

```text
Review all places where paid features are gated. Verify that enforcement happens on the server, not just in the UI. Find bypasses, race conditions, stale subscription state, and missing tests.
```

```text
Create a billing reconciliation plan. Include how to compare local subscription state with the payment provider, detect webhook misses, replay events safely, repair mismatches, and alert on money-impacting failures.
```

```text
Audit the checkout and subscription flows for production UX. Include loading states, failed payment states, duplicate submit prevention, invoice visibility, cancellation confirmation, plan downgrade warnings, and customer support handoff.
```

```text
Design billing analytics and finance operations for this app. Include MRR, ARR, churn, failed payments, refunds, credits, trials converting, plan distribution, usage overages, revenue leakage, and exports needed by finance.
```
