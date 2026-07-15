# /plan-team-claude

Claude-only architecture planning skill for **Claude Code** (also works in Cursor).

Same adversarial multi-team workflow as [`/plan-team`](../plan-team/), but every
candidate and synthesis agent uses a **different Claude model**.

## Install

From [jonathan-casca/skills](https://github.com/jonathan-casca/skills):

```bash
# Claude Code
cp -R plan-team-claude ~/.claude/skills/plan-team-claude
# or project-local
cp -R plan-team-claude <repo>/.claude/skills/plan-team-claude

# Cursor
cp -R plan-team-claude ~/.cursor/skills/plan-team-claude
```

Or add the whole repo as a Cursor Remote Rule:
`https://github.com/jonathan-casca/skills`

## Quick start

```text
/plan-team-claude Build a durable notification fan-out
/plan-team-claude Add Redis-backed membership tracking --mode lite
/plan-team-claude Design webhook retries --mode single
```

## Default Claude roster

### Cursor / Agent slugs

| Mode | Candidates | Synthesis |
| --- | --- | --- |
| `best` | `claude-opus-4-8-thinking-high`, `claude-sonnet-5-thinking-high`, `claude-4.6-opus-high-thinking`, `claude-4-sonnet` | `claude-opus-4-8-thinking-high` |
| `lite` | `claude-opus-4-8-thinking-high`, `claude-sonnet-5-thinking-high` | `claude-opus-4-8-thinking-high` |
| `single` | `claude-opus-4-8-thinking-high` | — |

### Claude Code aliases

When only aliases exist: `opus`, `sonnet`, `haiku` (still spawn isolated teams; prefer distinct IDs when available).

## Artifacts

```text
~/.claude/plan-team-runs/<timestamp>-<task-slug>/
<workspace>/.claude/plan-team-runs/<timestamp>-<task-slug>/
```

## Layout

```text
plan-team-claude/
├── SKILL.md
├── README.md
├── workflow.md
├── role-cards.md
├── output-contract.md
└── team-members/
```

See the shared [`plan-team` README](../plan-team/README.md) for modes, isolation rules, roster selection, and output contract details.
