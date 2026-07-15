---
name: plan-team-codex
description: Run GPT-only multi-agent architecture planning teams in Codex/Cursor using different OpenAI models, adversarial role debate, and a fresh synthesis plan. Use when the user invokes /plan-team-codex, wants Codex-native planning, or asks for GPT-model competing implementation plans.
disable-model-invocation: true
---

# Plan Team (Codex / GPT)

GPT-only architecture planning. Do not edit product code, create migrations, or
implement the final plan unless the user explicitly asks after reviewing it.

Prefer this skill inside **Codex CLI / Codex Desktop**. It also works in Cursor
when you want an all-GPT candidate roster.

## Modes

| Mode | Candidate teams | Final result |
|---|---:|---|
| `best` (default) | 4 GPT teams | Fresh GPT synthesis team combines 4 candidate plans |
| `lite` | 2 GPT teams | Fresh GPT synthesis team compares 2 candidate plans |
| `single` | 1 GPT team | Fresh GPT decision owner writes one plan |

Parse:

```text
/plan-team-codex <task> [--mode best|lite|single] [--plans N] [--models model1,model2,...] [--synth-model model] [--roles N] [--rounds N]
```

## Default GPT roster

Use **different GPT models** for candidates. Do not mix Claude/Grok/GLM into this skill.

```text
best candidates: gpt-5.6, gpt-5.4, gpt-5.6-terra, gpt-5.4-mini
best synthesis:  gpt-5.6

lite candidates: gpt-5.6, gpt-5.4
lite synthesis:  gpt-5.6

single team:     gpt-5.6
```

Reasoning effort defaults:

```text
gpt-5.6          → high
gpt-5.4          → high
gpt-5.6-terra    → medium
gpt-5.4-mini     → medium
```

Validate model IDs against the models available in the current Codex/Cursor
session. `--plans` must equal the number of supplied candidate models. For
`best`/`lite`, `--synth-model` is required only when overriding the candidate
roster. If a model is both candidate and synthesizer, synthesis agents must
still be newly spawned with no resumed context.

Optional research-preview substitute when available and the user asks for
latency over depth: `gpt-5.3-codex-spark` may replace `gpt-5.4-mini` only.

## Runtime (Codex)

- Spawn a **new Codex subagent** (or Cursor Task subagent) for every role, debate
  round, decision owner, and synthesis role.
- Never resume a prior agent/thread for a role turn.
- Pin `model` (and `model_reasoning_effort` in Codex agent configs) per the
  roster above.
- Keep subagents read-heavy / planning-focused (`sandbox_mode = "read-only"` in
  Codex when possible). Artifact writes are owned by the parent orchestrator.
- Run independent role agents and independent candidate teams in parallel.
- Run debate rounds only after all previous-round positions are available.

## Workflow

1. Read [workflow.md](workflow.md), [role-cards.md](role-cards.md), and [output-contract.md](output-contract.md).
2. Build the evidence packet before delegating.
3. Select only task-relevant roles. Include Security for auth/user-data/external APIs/tenant boundaries. Include Runtime/Scale for queues, Redis, caching, background work, or high volume.
4. Run one isolated GPT team per candidate model. Teams cannot see each other.
5. Run adversarial rounds with freshly spawned agents.
6. Spawn a fresh decision owner per candidate team for its standalone plan.
7. In `best`/`lite`, persist candidates, then run a fully fresh synthesis team on `gpt-5.6` (or override). A fresh decision owner writes the final build plan.
8. In `single`, skip cross-plan synthesis; spawn a fresh `gpt-5.6` decision owner for `final-plan.md`.
9. Persist artifacts to:

```text
~/.codex/plan-team-runs/<timestamp>-<task-slug>/
<workspace>/.codex/plan-team-runs/<timestamp>-<task-slug>/
```

Also mirror under `~/.cursor/plan-team-runs/...` when running inside Cursor if useful. Never put secrets, tokens, or unnecessary PII in artifacts.

## Team Size and Debate Defaults

- `best`: 5 roles per team and 2 debate rounds.
- `lite`: 4 roles per team and 1 debate round.
- `single`: 4 relevant roles and 1 debate round.
- Respect explicit `--roles` / `--rounds`. Do not pad with irrelevant roles.

## Decision Standard

```text
Correctness > Security > Reliability > Maintainability > Performance > DX > Speed
```

The final plan is not a vote. Reject weak proposals, reconcile trade-offs, preserve material dissent, and cite evidence or assumptions for consequential decisions.

## Queue / Redis / Runtime

Whenever the task touches queues, Redis, caching, membership tracking, scheduled jobs, notifications, event delivery, or scalable state, require Elena (Runtime/Scale) and the runtime analysis section in the output contract.

## Examples

```text
/plan-team-codex Build cross-model notification pages
/plan-team-codex Add a durable Redis-backed queue --mode lite
/plan-team-codex Design webhook retry delivery --mode single
/plan-team-codex Replace the task scheduler --mode best --rounds 3
/plan-team-codex Add tenant event processing --models gpt-5.6,gpt-5.4 --plans 2 --synth-model gpt-5.6
```
