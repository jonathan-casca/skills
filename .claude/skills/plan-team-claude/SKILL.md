---
name: plan-team-claude
description: Run Claude-only multi-agent architecture planning teams using different Claude models, adversarial role debate, and a fresh Opus synthesis plan. Use when the user invokes /plan-team-claude, wants Claude Code planning, or asks for Claude-model competing implementation plans.
disable-model-invocation: true
---

# Plan Team (Claude)

Claude-only architecture planning. Do not edit product code, create migrations, or
implement the final plan unless the user explicitly asks after reviewing it.

Prefer this skill inside **Claude Code**. It also works in Cursor when you want
an all-Claude candidate roster.

## Modes

| Mode | Candidate teams | Final result |
|---|---:|---|
| `best` (default) | 4 Claude teams | Fresh Opus synthesis team combines 4 candidate plans |
| `lite` | 2 Claude teams | Fresh Opus synthesis team compares 2 candidate plans |
| `single` | 1 Opus team | Fresh Opus decision owner writes one plan |

Parse:

```text
/plan-team-claude <task> [--mode best|lite|single] [--plans N] [--models model1,model2,...] [--synth-model model] [--roles N] [--rounds N]
```

## Default Claude roster

Use **different Claude models** for candidates. Do not mix GPT/Grok/GLM into this skill.

### Cursor / Agent model slugs

```text
best candidates: claude-opus-4-8-thinking-high, claude-sonnet-5-thinking-high,
                 claude-4.6-opus-high-thinking, claude-4-sonnet
best synthesis:  claude-opus-4-8-thinking-high

lite candidates: claude-opus-4-8-thinking-high, claude-sonnet-5-thinking-high
lite synthesis:  claude-opus-4-8-thinking-high

single team:     claude-opus-4-8-thinking-high
```

### Claude Code aliases (when running in Claude Code)

Map the roster to Claude Code model aliases if slugs above are unavailable:

```text
claude-opus-4-8-thinking-high / claude-4.6-opus-high-thinking → opus
claude-sonnet-5-thinking-high / claude-4-sonnet               → sonnet
optional fast filler when a 4th distinct Claude is needed     → haiku
```

If only `opus` / `sonnet` / `haiku` are available:

```text
best candidates: opus, sonnet, opus, haiku   # still spawn 4 isolated teams
best synthesis:  opus
lite candidates: opus, sonnet
lite synthesis:  opus
single team:     opus
```

Even when two teams share the `opus` alias, each team must be a newly spawned
agent with no shared context. Prefer distinct model IDs whenever the host exposes them.

Validate models against the current Claude Code / Cursor session. `--plans` must
equal the number of supplied candidate models. For `best`/`lite`, `--synth-model`
is required only when overriding the candidate roster.

## Runtime (Claude Code / Cursor)

- Spawn a **new** Claude Code agent/Task (or Cursor Task subagent) for every role,
  debate round, decision owner, and synthesis role.
- Never resume a prior agent for a role turn.
- Pin the model per the roster above (`model:` on Claude Code agents / Task model
  slug in Cursor).
- Keep role agents planning-focused; the parent orchestrator owns artifact writes.
- Run independent role agents and independent candidate teams in parallel.
- Run debate rounds only after all previous-round positions are available.

## Workflow

1. Read [workflow.md](workflow.md), [role-cards.md](role-cards.md), and [output-contract.md](output-contract.md).
2. Build the evidence packet before delegating.
3. Select only task-relevant roles. Include Security for auth/user-data/external APIs/tenant boundaries. Include Runtime/Scale for queues, Redis, caching, background work, or high volume.
4. Run one isolated Claude team per candidate model. Teams cannot see each other.
5. Run adversarial rounds with freshly spawned agents.
6. Spawn a fresh decision owner per candidate team for its standalone plan.
7. In `best`/`lite`, persist candidates, then run a fully fresh synthesis team on Opus. A fresh decision owner writes the final build plan.
8. In `single`, skip cross-plan synthesis; spawn a fresh Opus decision owner for `final-plan.md`.
9. Persist artifacts to:

```text
~/.claude/plan-team-runs/<timestamp>-<task-slug>/
<workspace>/.claude/plan-team-runs/<timestamp>-<task-slug>/
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
/plan-team-claude Build cross-model notification pages
/plan-team-claude Add a durable Redis-backed queue --mode lite
/plan-team-claude Design webhook retry delivery --mode single
/plan-team-claude Replace the task scheduler --mode best --rounds 3
/plan-team-claude Add tenant event processing --models claude-opus-4-8-thinking-high,claude-sonnet-5-thinking-high --plans 2 --synth-model claude-opus-4-8-thinking-high
```
