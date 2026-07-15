# Execution Workflow

## 1. Build the Evidence Packet

Inspect only code and documents relevant to the task. The packet must contain:

```markdown
# Evidence Packet

## User goal
[Verbatim task and stated outcomes]

## Existing behavior
- [Verified fact] — [file:line-range]

## Relevant boundaries
- [Auth, tenant, data, runtime, UI, external systems]

## Constraints
- [Repository instructions, compatibility, scale, migration, deadlines]

## Unknowns and assumptions
- [Unknown] — [safe default or question required]
```

Do not claim a symbol, API, schema, capacity, or deployment detail exists unless it was verified.

## 2. Candidate Team Formation

For each candidate model:

1. Select task-relevant team members using `role-cards.md`, then read each selected brief in `team-members/`.
2. Spawn one fresh subagent for each selected role in parallel.
3. Use the candidate model for every role in that candidate team.
4. Include the role card, task, evidence packet, and role-position contract below in every prompt.
5. Do not share any other candidate team's output.

### Initial Role Prompt

```markdown
You are the [ROLE] in Candidate Team [N].

You have a fresh context window. You may use only this prompt's task and evidence;
do not assume other agents have investigated anything for you.

## Task
[VERBATIM USER TASK]

## Evidence Packet
[PACKET]

## Role Card
[ROLE CARD]

## Assignment
Form an independent position. Separate verified facts from assumptions. If an
architectural choice depends on an unknown, name the exact measurement, repository
inspection, or user decision that would resolve it.

Return exactly:
## [ROLE] — Initial Position
### Verified observations
### Proposed architecture
### API and domain implications
### Data and runtime implications
### Security and reliability implications
### Risks and failure modes
### Non-negotiable requirements
### Assumptions
### Challenge question for another role
```

## 3. Adversarial Discussion

When every initial position is available, construct a discussion packet for each role containing:

- the evidence packet;
- that role's prior position;
- every peer's prior position, labeled by role;
- the role's compact card.

Spawn a **new** agent for every role. Never resume an old agent.

### Debate Prompt

```markdown
You are the [ROLE] in Candidate Team [N], adversarial round [R].

This is a new context window. Your prior position and all peer positions are
included below; nothing else may be assumed.

## Evidence Packet
[PACKET]

## Your Role Card
[ROLE CARD]

## Your Prior Position
[POSITION]

## Peer Positions
[LABELED POSITIONS]

## Assignment
Challenge the most consequential unsupported, unsafe, or incomplete proposal.
Concede only with evidence. Resolve inconsistencies across API, data, security,
and runtime design. Do not repeat general principles.

Return exactly:
## [ROLE] — Round [R]
### Challenge
[Quote the claim and explain the issue]
### Defense or concession
### Cross-cutting consequence
### Revised recommendation
### Evidence gaps or validation
### Remaining dissent
```

## 4. Candidate Team Decision Owner

After final debate positions are available, spawn a new decision owner with the same candidate model. It receives the evidence packet and only its candidate team's positions/debate.

The owner writes a standalone candidate plan using `output-contract.md`. It must resolve disagreements by the decision hierarchy and preserve dissent that could change the decision after measurement.

## 5. Fresh Synthesis Team

For `best` and `lite` only:

1. Persist the evidence packet, discussions, and candidate plans.
2. Select fresh roles relevant to the task; do not blindly reuse the candidate selection.
3. Spawn fresh synthesis-role agents with the synthesis model in parallel. Each receives the evidence packet, compact role card, and all candidate plans.
4. Each synthesis role first audits the evidence independently, then compares candidate claims.
5. Run configured adversarial rounds with newly spawned synthesis agents.
6. Spawn a fresh final decision owner to write the final plan using `output-contract.md`.

### Synthesis Role Prompt

```markdown
You are the [ROLE] in the Final Synthesis Team.

You have a fresh context window. Candidate plans are proposals, not truth. Audit
them against the evidence packet before accepting any claim.

## Task
[VERBATIM USER TASK]

## Evidence Packet
[PACKET]

## Role Card
[ROLE CARD]

## Candidate Plans
[LABELED CANDIDATE PLANS]

## Assignment
Identify the strongest and weakest proposal for your specialty. Reconcile only
where the evidence supports it. State unresolved assumptions, material dissent,
and the best validation step.

Return exactly:
## [ROLE] — Synthesis Position
### Evidence audit
### Best-supported proposal
### Rejected proposal and reason
### Required guardrails
### Open validation
```

## 6. Single Mode

Run one Opus team with the selected roles and one adversarial round. Do not create candidate-plan comparison or a synthesis team. Spawn a new Opus decision owner after the discussion to create `final-plan.md`.

## 7. Artifact Persistence

Use a UTC timestamp and sanitized task slug. Create both run roots:

```text
~/.cursor/plan-team-runs/<timestamp>-<task-slug>/
<workspace>/.cursor/plan-team-runs/<timestamp>-<task-slug>/
```

Write identical Markdown content to both roots:

```text
run-manifest.md
evidence-packet.md
candidate-01.md ... candidate-NN.md
candidate-01-discussion.md ... candidate-NN-discussion.md
final-synthesis-discussion.md            # best/lite only
final-synthesis.md                       # best/lite only
final-plan.md                            # single only
decision-ledger.md
```

If a write fails, report the failed path and preserve the plan output in chat; do not claim the artifacts were saved.
