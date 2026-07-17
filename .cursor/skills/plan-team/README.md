# /plan-team

Multi-model architecture planning skill for [Cursor](https://cursor.com) Agent.

Spawns **isolated architecture teams** that investigate a software task, debate with
task-selected specialist roles, write competing candidate plans, then produce a
**fresh final build plan**. Planning only — it does not edit product code, create
migrations, or implement the plan unless you explicitly ask after review.

Repo: [jonathan-casca/skills](https://github.com/jonathan-casca/skills)

---

## Install

### Option A — Remote Rule (GitHub)

1. Open **Customize → Rules** in Cursor
2. **Add Rule → Remote Rule (GitHub)**
3. Paste:

```text
https://github.com/jonathan-casca/skills
```

4. Reload Agent chat and run `/plan-team <task>`

### Option B — Copy into skills folder

```bash
git clone https://github.com/jonathan-casca/skills.git
cp -R skills/plan-team ~/.cursor/skills/plan-team
# or, for one repo only:
cp -R skills/plan-team <your-repo>/.cursor/skills/plan-team
```

---

## Quick start

```text
/plan-team Build cross-model notification pages
/plan-team Add a durable Redis-backed queue --mode lite
/plan-team Design webhook retry delivery --mode single
/plan-team Replace the task scheduler --mode best --rounds 3
/plan-team Add tenant event processing --models claude-opus-4-8-thinking-high,glm-5.2-high --plans 2 --synth-model gpt-5.6-luna-medium
```

### CLI shape

```text
/plan-team <task> [--mode best|lite|single] [--plans N] [--models model1,model2,...] [--synth-model model] [--roles N] [--rounds N]
```

| Flag | Meaning |
| --- | --- |
| `--mode` | `best` (default), `lite`, or `single` |
| `--plans` | Number of candidate teams (must match `--models` count) |
| `--models` | Comma-separated candidate model slugs |
| `--synth-model` | Synthesis model (required when overriding candidates in `best`/`lite`) |
| `--roles` | Cap on roles per team |
| `--rounds` | Adversarial debate rounds per candidate team |

---

## Modes

| Mode | Candidate teams | Final result |
| --- | ---: | --- |
| `best` (default) | 4 teams | Fresh synthesis team combines 4 candidate plans |
| `lite` | 2 teams | Fresh synthesis team compares 2 candidate plans |
| `single` | 1 Opus team | Fresh Opus decision owner writes one plan |

### Default model roster

```text
best candidates: gpt-5.6-terra-medium, claude-opus-4-8-thinking-high,
                 cursor-grok-4.5-high-fast, glm-5.2-high
best synthesis:  claude-opus-4-8-thinking-high

lite candidates: claude-opus-4-8-thinking-high, cursor-grok-4.5-high-fast
lite synthesis:  gpt-5.6-luna-medium

single team:     claude-opus-4-8-thinking-high
```

Defaults for team size / debate:

- `best`: ~5 roles, 2 debate rounds
- `lite` / `single`: ~4 roles, 1 debate round

---

## How it works

1. **Evidence packet** — bounded factual digest of the request, relevant code/docs, constraints, and unknowns (with file:line cites).
2. **Role selection** — only specialists who own a real risk for this task (see roster below).
3. **Candidate teams** — one isolated team per model; teams cannot see each other.
4. **Adversarial debate** — fresh subagents each round; no `resume`, no shared context windows.
5. **Candidate plans** — each team’s decision owner writes a standalone build plan.
6. **Synthesis** (`best` / `lite`) — a fully fresh team reviews evidence + candidates, then a fresh decision owner writes the final plan.
7. **Artifacts** — plans are persisted under:

```text
<workspace>/.cursor/plan-team-runs/<timestamp>-<task-slug>/   # always
~/.cursor/plan-team-runs/<timestamp>-<task-slug>/             # when ~/.cursor is writable
```

### Isolation rules (non-negotiable)

- New subagent for every role, debate round, decision owner, and synthesis role
- Never `resume` or reuse a role agent’s context
- Self-contained prompts only
- Desktop: local foreground subagents. Cloud / remote serverless: run subagents in the host environment (do not nest extra cloud VMs from Desktop)

### Decision standard

```text
Correctness > Security > Reliability > Maintainability > Performance > DX > Speed
```

The final plan is **not a vote**. It must reject weak proposals, reconcile trade-offs, preserve important dissent, and cite evidence or assumptions for consequential choices.

---

## Team roster

| Member | Owns | Select when |
| --- | --- | --- |
| Ada Chen — Systems | Boundaries, duplicate authority, derived state | Always |
| Maya Patel — Delivery/Verification | Proof, tests, rollout | Always |
| Iris Gomez — Reuse | Rebuild vs reuse risk | Large/legacy codebases, shared primitives |
| Marcus Reed — Domain/API | Command/query contracts | New APIs, domain flows, UI mutations |
| Priya Nair — Data/Lifecycle | Schema, migrations, durability | Persistence, history, workers |
| Elena Kovacs — Runtime/Scale | Queues, Redis, fan-out, backpressure | Async, cache, notifications, scale |
| Omar Hassan — Multi-Tenancy | Cross-tenant leakage | Org/tenant data, roles/grants |
| Nadia Volkov — Security | Authz, secrets, unsafe input | Auth, PII, webhooks, deep links |
| Caleb Ward — Reliability | Ops, observability, recovery | Multi-service, criticality, deploys |
| Sofia Ibarra — Integrations | Vendor contracts, replay | External APIs, import/export |

Queue / Redis / cache / scheduled jobs / notifications always require **Elena** and the runtime analysis section in the output contract.

Full cards live in [`team-members/`](./team-members/).

---

## What you get

Every candidate and final plan follows [`output-contract.md`](./output-contract.md):

- Decision summary + confidence
- Current state and evidence cites
- Architecture (boundaries, flows, auth/tenancy)
- API structure
- Data model and lifecycle
- Runtime / queue / Redis / cache analysis (when relevant)
- Failure modes, tests, rollout, open questions

---

## Layout

```text
plan-team/
├── README.md                # this file
├── SKILL.md                 # slash-command entrypoint for Cursor
├── workflow.md              # phase-by-phase orchestration
├── role-cards.md            # selection table + rules
├── output-contract.md       # required plan sections
└── team-members/            # per-role specialist briefs
```

Also mirrored at [`.cursor/skills/plan-team/`](../.cursor/skills/plan-team/) for Cursor project discovery.

---

## Requirements

- Cursor Agent with subagents (Desktop or Cloud / remote serverless)
- For Cloud: install via **Customize → Rules → Remote Rule (GitHub)** → `https://github.com/jonathan-casca/skills` (project `.cursor/skills` is often gitignored and unavailable on cloud VMs)
- Models from the currently available subagent model list (slugs validated at run time)
- Do not put secrets, tokens, or unnecessary PII into plan artifacts

---

## License

MIT — see the [repo LICENSE](../LICENSE).
