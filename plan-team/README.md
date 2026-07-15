# /plan-team

Multi-model architecture planning skill for Cursor Agent.

Spawns isolated architecture teams that investigate a software task, debate with
task-selected roles, write competing candidate plans, and produce a fresh final
build plan. Planning only — it does not edit product code unless you ask after review.

## Install

From the parent repo:

```text
https://github.com/jonathan-casca/skills
```

Or copy this folder to:

```text
~/.cursor/skills/plan-team/
# or
<your-repo>/.cursor/skills/plan-team/
```

Then in Cursor Agent chat:

```text
/plan-team <task>
/plan-team Add a durable Redis-backed queue --mode lite
/plan-team Design webhook retry delivery --mode single
```

## Modes

| Mode | Candidate teams | Final result |
| --- | ---: | --- |
| `best` (default) | 4 teams | Fresh synthesis team combines 4 candidate plans |
| `lite` | 2 teams | Fresh synthesis team compares 2 candidate plans |
| `single` | 1 Opus team | Fresh Opus decision owner writes one plan |

## Layout

```text
plan-team/
├── SKILL.md                 # slash-command entrypoint
├── workflow.md              # phase-by-phase orchestration
├── role-cards.md            # role selection + card map
├── output-contract.md       # required plan sections
└── team-members/            # per-role specialist cards
```

## Notes

- Requires Cursor Desktop with local subagents (not cloud agents).
- Candidate/synthesis model defaults are listed in `SKILL.md`.
- Artifacts are written under `.cursor/plan-team-runs/` (workspace + home).
