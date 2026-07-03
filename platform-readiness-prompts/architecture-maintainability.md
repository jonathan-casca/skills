# Architecture And Maintainability Prompts

```text
Review this codebase for architecture problems that will slow future development. Look for large files, mixed concerns, business logic in UI/API handlers, duplicated logic, weak types, and unclear module boundaries.
```

```text
Refactor plan: identify the top 5 modules that should be split, renamed, or reorganized before the app grows. Keep the plan pragmatic and avoid premature abstraction.
```

```text
Find places where business rules are duplicated across frontend, backend, and tests. Propose a single source of truth.
```

```text
Review TypeScript usage. Find unsafe any, weak types, ignored errors, type assertions, nullable footguns, and places where stronger domain types would prevent bugs.
```
