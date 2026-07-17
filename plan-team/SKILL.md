---
name: plan-team
description: Run multi-model architecture planning teams that independently investigate a software task, debate it with task-selected architecture roles, save candidate plans, and produce a fresh final build plan. Use when the user invokes /plan-team, asks for competing implementation plans, deep system design, queue or Redis architecture, or a multi-agent planning debate.
disable-model-invocation: true
---

# Plan Team

Use this skill only for planning. Do not edit product code, create migrations, or implement the final plan unless the user explicitly asks after reviewing it.

## Modes

| Mode | Candidate teams | Final result |
|---|---:|---|
| `best` (default) | 4 teams | Fresh synthesis team combines 4 candidate plans |
| `lite` | 2 teams | Fresh synthesis team compares 2 candidate plans |
| `single` | 1 Opus team | Fresh Opus decision owner writes one plan |

Parse:

```text
/plan-team <task> [--mode best|lite|single] [--plans N] [--models model1,model2,...] [--synth-model model] [--roles N] [--rounds N]
```

Defaults:

```text
best candidates: gpt-5.6-terra-medium, claude-opus-4-8-thinking-high,
                 cursor-grok-4.5-high-fast, glm-5.2-high
best synthesis:  claude-opus-4-8-thinking-high

lite candidates: claude-opus-4-8-thinking-high, cursor-grok-4.5-high-fast
lite synthesis:  gpt-5.6-luna-medium

single team:     claude-opus-4-8-thinking-high
```

Use the fixed roster unless the user supplies overrides. Validate model slugs against the currently available subagent-model list. `--plans` must equal the number of supplied candidate models. For `best`/`lite`, `--synth-model` is required only when overriding the candidate roster. If a model appears as both candidate and synthesizer, the synthesis agents must still be newly spawned with no resumed context.

## Non-negotiable Isolation

- Spawn a new subagent for every role, every debate round, every team decision owner, and every synthesis role.
- Never use `resume`. Never reuse a role agent's context window.
- Give every new agent a self-contained prompt with only the evidence it needs.
- Run independent role agents and independent candidate teams in parallel.
- Run debate rounds only after all previous-round positions are available.
- Prefer Cursor Desktop foreground subagents when the host session is local. When the host is already a Cloud / remote serverless agent, run planning subagents in that same environment — do not nest extra cloud VMs from Desktop, and do not refuse to run solely because the host is serverless.

## Workflow

1. Read [workflow.md](workflow.md), [role-cards.md](role-cards.md), and [output-contract.md](output-contract.md).
2. Build the evidence packet before delegating. It must be a bounded, factual digest of the user request, relevant code/docs, architecture constraints, data flows, existing tests, and unresolved choices. Cite file paths and line ranges where available.
3. Select only the roles relevant to the task. Include Security for any auth, user-data, external API, or tenant boundary. Include Scalability and Runtime for queues, Redis, caching, background work, state tracking, or expected high volume.
4. Run one isolated architecture team for each candidate model. Each team receives the same evidence packet and selected roles, but cannot see other teams.
5. Run the configured adversarial rounds inside each candidate team. Require specific challenges and evidence-backed revisions.
6. Spawn a fresh decision owner for each candidate team to write its standalone candidate plan.
7. In `best` and `lite`, persist all candidate artifacts, then run a fully fresh synthesis team. It first independently reviews the evidence, then critiques the candidate plans. A fresh decision owner writes the single final build plan.
8. In `single`, skip cross-plan synthesis. Spawn a fresh Opus decision owner after the one team discussion to write the final build plan.
9. Persist artifacts, then return links to the final plan and candidate plans:

```text
<workspace>/.cursor/plan-team-runs/<timestamp>-<task-slug>/   # always (Cloud + Desktop)
~/.cursor/plan-team-runs/<timestamp>-<task-slug>/             # also write when home is writable (Desktop)
```

On Cloud / remote serverless hosts, home (`~/.cursor`) may be missing or ephemeral — workspace persistence is required; skip the personal mirror if `~/.cursor` is not writable. Use a slug made only of lowercase letters, numbers, and hyphens. Never put secrets, raw tokens, or unnecessary PII in artifacts.

## Team Size and Debate Defaults

- `best`: 5 roles per team and 2 debate rounds.
- `lite`: 4 roles per team and 1 debate round.
- `single`: 4 relevant roles and 1 debate round.
- Respect explicit `--roles` and `--rounds` values. Do not add irrelevant roles merely to reach a count.

## Decision Standard

The final decision owner must prefer:

```text
Correctness > Security > Reliability > Maintainability > Performance > DX > Speed
```

The final plan is not a vote. It must independently reject weak proposals, reconcile real trade-offs, preserve important dissent, and name the evidence or assumption behind each consequential decision.

## Queue, Redis, and Runtime Requirement

Whenever a task touches queues, Redis, caching, membership tracking, scheduled jobs, notifications, event delivery, or scalable state, require the Scalability and Runtime role and the runtime analysis in the output contract. Do not accept “use Redis” or “use a queue” without workload, consistency, ownership, failure, and recovery analysis.

## Missing Information

If a missing decision changes the architecture materially, ask the user one focused question before launching teams. Otherwise label the uncertainty as an assumption and require every plan to state how it would validate it.

## Examples

```text
/plan-team Build cross-model notification pages
/plan-team Add a durable Redis-backed queue --mode lite
/plan-team Design webhook retry delivery --mode single
/plan-team Replace the task scheduler --mode best --rounds 3
/plan-team Add tenant event processing --models claude-opus-4-8-thinking-high,glm-5.2-high --plans 2 --synth-model gpt-5.6-luna-medium
```
