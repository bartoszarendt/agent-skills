---
name: planning
description: Turn an outcome into a proportionate implementation plan with dependencies, observable acceptance criteria, and evidence of completion. Use when asked for a plan or when work has multiple dependent outcomes, material uncertainty, or spans sessions.
---

# Planning

Record the decisions needed to implement the requested outcome correctly.
Keep the plan small enough to use and detailed enough to prevent materially
different interpretations.

## Establish the contract

Read the request, applicable instructions, existing plan, and relevant code.
Identify the outcome, constraints, existing mechanisms, and commitments to users
or consumers. Separate verified facts, assumptions, and unresolved decisions.

A request for a plan does not authorize implementation. When a plan is part of
already-authorized implementation, continue after resolving material blockers;
do not introduce another approval gate. Preserve any explicit review gates.

Ask about unresolved choices that change the outcome, contracts, persisted data,
security, significant cost, or irreversible behavior. Make routine choices from
repository evidence. Continue independent work while a dependent choice waits.

## Choose the smallest useful form

- For one coherent change, use a short statement of intent, affected area, and
  verification. A separate document or task table may add no value.
- For several dependent outcomes, use an ordered task list with acceptance and
  dependencies.
- For work spanning phases or sessions, keep a compact roadmap linking to phase
  files. Keep current detail in the relevant phase rather than copying it into
  the roadmap.
- Keep distant work at the level of goals, scope, risks, and decisions. Expand it
  when it approaches implementation.

Follow the project's existing format and source of truth. For larger work or
tasks with interpretation risk, adapt
[references/plan-format.md](references/plan-format.md). Omit unused sections.

## Define coherent tasks

Prefer a complete observable behavior or a resolved risk per task. A schema,
endpoint, and UI for one behavior may form one task. File count, line count, and
the word "and" do not determine the boundary.

Put consequential unknowns early. Discover existing interfaces before proposing
new ones. Use an agreed contract first when independent implementations need it.
For changes with real compatibility commitments, consider an additive transition
and explicit removal conditions. Do not add migration machinery without a need.

Include restructuring that is necessary for a coherent solution. Separate it
when that makes review or verification materially easier, rather than making
separate tasks or commits mandatory.

For each task, state:

- the result and why it matters;
- dependencies that actually block it;
- observable acceptance criteria;
- the evidence that would establish success.

Use exact commands when known and useful. If commands depend on later discovery,
state the required scenario and outcome, and identify who will resolve execution
details. Do not replace a meaningful proof with "run tests."

## Add detail where interpretation matters

Add a task-detail block when the task:

- establishes a contract consumed by later work;
- introduces or materially changes behavior across a public interface,
  persistence, migration, security, isolation, or destructive-operation boundary;
- preserves a non-obvious compatibility or architectural decision;
- permits plausible interpretations that would miss the intended outcome; or
- could pass ordinary happy-path checks while still failing its purpose.

Record the observable contract, deliberate boundaries, relevant decisions,
existing mechanisms to inspect, required proof, and a likely misleading result.
Use a "Misfire" field to name how work could appear complete while missing intent.
Routine mechanical tasks need no such block.

An edit inside a boundary does not automatically require more documentation.
Reuse existing acceptance and proof when they already express the contract; a
few explicit lines can be sufficient without duplicating them under every field.

Record decisions and reasons where they constrain implementation. Mark a decision
as locked only when the user or project has actually established that commitment.
Include rejected alternatives when their rationale is likely to matter again.

## Preserve intent through execution

The plan owns the intended outcome, exclusions, binding decisions, and required
strength of evidence. The executor determines current files, commands, and
implementation steps from repository evidence.

When creating separate task records, cite the source plan, task ID, and revision
or date. Preserve binding contract and boundary text; add operational detail
without weakening it. If splitting a task, map the children to all parent
requirements and name any proposed deferral.

Treat file and module anchors as evidence to inspect, not an exclusive edit list.
Explain a replacement when an anchor is stale. Amend consequential ambiguity
before dependent implementation; use an existing change-request gate when a
locked decision would change.

Direct execution from the plan is sufficient. Do not introduce a tracker or
duplicate task records solely to follow this process. External task creation
requires authorization covering that action.

## Track acceptance and closeout

Map every acceptance criterion to a task contract or an explicit integration
gate with an owner. Several tasks can contribute to one outcome.

Record material deviations and their reasons in the existing plan. Preserve
unrelated unfinished work and historical evidence. Add a dated correction when
later results supersede an earlier closeout.

Distinguish implemented, verified, deployed, blocked, and deferred work. Mark a
phase done only when its required acceptance and gates are satisfied. A user
decision to defer work changes the recorded scope; a skipped check is not a pass.
On completion, keep a short dated roadmap entry with a commit or artifact anchor
when available, and retain detailed evidence in the phase file.

## Verification

- [ ] The format and detail match the size and risk of the work.
- [ ] Every requirement maps to a task or explicit gate; proposed exclusions are visible.
- [ ] Dependencies and unresolved decisions identify what they block.
- [ ] Tasks with interpretation risk preserve contracts, boundaries, and proof.
- [ ] Verification is proportionate and does not automatically require new tests.
- [ ] Existing authorization and explicit project gates are respected.
- [ ] The plan has one maintained source of truth and an honest completion state.
