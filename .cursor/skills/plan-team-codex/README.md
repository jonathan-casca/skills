# /plan-team-codex

GPT-only architecture planning skill for **Codex CLI / Codex Desktop** (also works in Cursor).

Same adversarial multi-team workflow as [`/plan-team`](../plan-team/), but every
candidate and synthesis agent uses a **different OpenAI GPT model**.

## Install

From [jonathan-casca/skills](https://github.com/jonathan-casca/skills):

```bash
# Codex
cp -R plan-team-codex ~/.codex/skills/plan-team-codex
# or project-local
cp -R plan-team-codex <repo>/.codex/skills/plan-team-codex

# Cursor
cp -R plan-team-codex ~/.cursor/skills/plan-team-codex
```

Or add the whole repo as a Cursor Remote Rule:
`https://github.com/jonathan-casca/skills`

## Quick start

```text
/plan-team-codex Build a durable notification fan-out
/plan-team-codex Add Redis-backed membership tracking --mode lite
/plan-team-codex Design webhook retries --mode single
```

## Default GPT roster

| Mode | Candidates | Synthesis |
| --- | --- | --- |
| `best` | `gpt-5.6`, `gpt-5.4`, `gpt-5.6-terra`, `gpt-5.4-mini` | `gpt-5.6` |
| `lite` | `gpt-5.6`, `gpt-5.4` | `gpt-5.6` |
| `single` | `gpt-5.6` | — |

Reasoning effort: `gpt-5.6`/`gpt-5.4` → high; `gpt-5.6-terra`/`gpt-5.4-mini` → medium.

## Artifacts

```text
~/.codex/plan-team-runs/<timestamp>-<task-slug>/
<workspace>/.codex/plan-team-runs/<timestamp>-<task-slug>/
```

## Layout

```text
plan-team-codex/
├── SKILL.md
├── README.md
├── workflow.md
├── role-cards.md
├── output-contract.md
└── team-members/
```

See the shared [`plan-team` README](../plan-team/README.md) for modes, isolation rules, roster selection, and output contract details.
