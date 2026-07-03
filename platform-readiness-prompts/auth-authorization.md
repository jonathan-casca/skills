# Auth And Authorization Prompts

```text
Audit all API endpoints and server actions for authentication and authorization gaps. Find any place where existence is checked without ownership, any public endpoint that should be protected, and any missing org/tenant boundary checks.
```

```text
Review this app for multi-tenant data isolation bugs. Find every query that touches user/org/customer data and verify it scopes by the authenticated principal. Return exact risky locations and recommended fixes.
```

```text
Design a proper authorization layer for this app. Include roles, permissions, tenant/org boundaries, resource ownership checks, and where each check should live.
```

```text
Find all places where the frontend hides functionality but the backend does not enforce authorization. Propose backend-side enforcement.
```
