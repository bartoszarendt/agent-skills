# Plan format

Use the project's established template first. Adapt the following forms when
they help preserve intent. Do not create phase files or identifiers for work
that fits a short task description.

## Small change

```markdown
Goal: Reject an expired invitation without creating membership.
Approach: Use the existing invitation acceptance transaction.
Acceptance: An expired invitation returns the established error and creates no member.
Verify: Run the existing invitation acceptance cases; inspect missing coverage
before extending them.
```

## Phase

```markdown
# Phase N: <outcome>

Status: planned | in progress | blocked | done (<date>)
Goal: <observable outcome and why it matters>
Dependencies: <prior work or external prerequisites, or none>

## Decisions
- DN-1: <binding choice, with its authority or proposed status>
  - Rationale: <why it is needed>
  - Rejected: <alternative and reason, only when useful>

## Scope
- <included work>

## Boundaries
- <deliberate exclusions and operational constraints>

## Tasks
| ID | Status | Task | Intent | Depends on |
|---|---|---|---|---|
| PN-01 | open | <action> | <result, so that...> | none |

## Task detail
### PN-01: <title>
- Contract:
  - PN-01-C1: <observable outcome>
  - PN-01-C2: <consequential edge or failure behavior>
- Boundaries:
  - PN-01-B1: <task-specific exclusion>
- Binds: <relevant decision IDs>
- Anchors: <existing mechanisms to inspect>
- Proof: <scenario and evidence required>
- Misfire: <plausible result that would miss the intended outcome>

## Acceptance
- PN-A1: <phase outcome> -> PN-01/PN-01-C1
- PN-A2: <integration outcome> -> <gate and responsible task or owner>

## Verification
- <required scenarios, environment, and deliberately fixed commands>
- <access, authorization, or environment prerequisites>

## Open questions
- <decision, consequence, and affected task>

## Closeout
- <date, delivered scope, and relevant revision or artifact>
- <commands or runtime checks, results, and environment>
- <unmet gates, agreed deferrals, and follow-up ownership>
```

Omit empty sections and task details that add no protection. Add sequencing
notes only when the dependency table cannot express the constraint. Keep a
roadmap's entries short and link to these phase records.

## Detail example

```markdown
### P3-02: Accept an invitation once

- Contract:
  - P3-02-C1: Repeating acceptance returns the existing membership.
  - P3-02-C2: Concurrent acceptance creates at most one membership.
  - P3-02-C3: An expired or revoked invitation creates no membership.
- Boundaries:
  - P3-02-B1: Do not alter existing role assignments.
- Anchors: Invitation service, membership transaction, uniqueness constraint.
- Proof: Exercise repeated and overlapping requests against the persistence
  boundary. Reuse existing cases where they establish these outcomes.
- Misfire: A sequential happy-path test passes while concurrent requests create
  duplicate memberships.
```

The contract constrains the result without prescribing a particular helper or
locking a stale filename. If a required scenario cannot run, record the gap;
a lower-fidelity substitute does not silently discharge the gate.

## Derived tasks

When a separate task record is useful, include:

- source phase and task ID, plus revision or dated version;
- the exact binding contract and boundary text carried by the task;
- discovered implementation areas and concrete execution commands;
- verification results and deviations.

When splitting a source task, preserve coverage across all children. Keep shared
proof as an explicit integration gate if no child can establish it alone.
Do not copy a mutable status checklist into several places.

## Amendments

Preserve the distinction between a proposal and an approved change of scope.
For a material change, record what changed, why, who or what authorized it,
which criteria are affected, and what evidence must be refreshed. Keep prior
results dated so they cannot be mistaken for verification of the new state.
