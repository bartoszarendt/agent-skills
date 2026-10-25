---
name: planning
description: Plan multi-step work before implementing it — sequence steps and dependencies, identify work that can proceed in parallel, surface unknowns and decisions, and define acceptance criteria and proportionate verification. Use when a feature, fix, refactor, migration, or other task needs several coordinated steps, when given a spec or requirements, when asked for a plan, breakdown, or roadmap, or when uncertainty or work across sessions makes an explicit approach useful. Scales from a brief outline to a detailed plan.
---

# Planning

Record the decisions needed to implement the requested outcome correctly.
Keep the plan small enough to use and detailed enough to prevent materially
different interpretations.

Before implementing multi-step work, assess sequencing, dependencies, unknowns,
and verification. When the approach is clear, a brief outline is enough;
continue into any authorized implementation. Expand detail only where it
prevents a consequential omission or misunderstanding.

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

Before the plan is approved, surface any substantial involvement it needs from
the user, such as a decision, an action, a review, or labor, with its purpose
and the alternatives, including what an agent could do with the access the work
already has, such as research or a bounded observation. An agent route still
needs the authorization the action itself needs.

Before breaking down the work, separate the required outcome from the
mechanisms proposed to reach it. For each new service, dependency, abstraction,
configuration, migration path, or process step, name the current requirement it
serves and check whether an existing mechanism or platform capability meets it.
Do not narrow the user's outcome to shrink the plan; present a narrower option
as a choice with its trade-off.

## Choose the smallest useful form

- For one coherent change, use a short statement of intent, affected area, and
  verification. A separate document or task table may add no value.
- For multiple steps that benefit from explicit ordering or tracking, use an
  ordered list. Give each step its result and check, and name dependencies
  where they block.
- For larger work, group tasks into work units. Keep a concise overview linked
  to detailed unit records when that separation helps, with current detail in
  the unit record rather than copied into the overview. Work across sessions
  does not by itself require several files.
- Keep distant work at the level of goals, scope, risks, and decisions. Expand it
  when it approaches implementation.

A brief ordered plan for one feature:

```markdown
1. Add the digest frequency setting to the existing settings schema with its
   default. Check: schema cases cover the default.
2. Persist it through the current preferences store. Check: a saved value
   survives reload.
3. Expose it on the notification settings screen. Check: changing it in the
   UI updates the stored value.
```

Follow the project's existing format and source of truth. Inspect applicable
instructions and representative current plans or work records for naming and
numbering conventions. Preserve their hierarchy, prefixes, numbering, and
relationships between work units, tasks, contracts, decisions, and acceptance
criteria. Continue established identifiers rather than renaming existing
records to match a template.

Without an established convention, use phases containing tasks when the scope
warrants structured planning. Use phase-qualified identifiers consistently,
such as `P3-02` for a task and `P3-02-C1` for its first contract. Small changes
can still use a brief outline without phases or identifiers.

For larger work or tasks with interpretation risk, adapt
[references/plan-format.md](references/plan-format.md). Omit unused sections.

## Define coherent tasks

Prefer a complete observable behavior or a resolved risk per task. A schema,
endpoint, and UI for one behavior may form one task. File count, line count, and
the word "and" do not determine the boundary.

Put consequential unknowns early. Run the step whose result could change the
design, such as the real operation under its failure conditions, before building
proof or instruments around it. A probe that ships and enables nothing can run
ahead of the work it informs when it stays within existing authorization and
approved decisions and keeps off shared resources; one that cannot is the
change to propose. Discover existing interfaces before proposing
new ones. Use an agreed contract first when independent implementations need it.
For changes with real compatibility commitments, consider an additive transition
and explicit removal conditions. Do not add migration machinery without a need.
When a change crosses a deployment boundary or cannot be fully undone, such as a
data migration or a contract other systems consume, order the work so each
deployed step leaves the system working. State the deployment order, how long
old and new forms coexist, and the point after which rolling back no longer
restores the previous state, with the recovery path beyond it.

Identify work that can proceed independently. Where practical, organize tasks so
independent work can run in parallel without weakening coherent outcomes:
establish shared contracts first, name conflicting edits or shared mutable
resources, and state where results are integrated and verified. Keep work
sequential when dependencies, coordination cost, or interference outweigh the
benefit. Identifying parallel opportunities does not authorize launching agents
or external processes; keep the plan usable for sequential or parallel
execution within existing authorization and available capabilities.

Include restructuring that is necessary for a coherent solution. Separate it
when that makes review or verification materially easier, rather than making
separate tasks or commits mandatory.

For each task, state the following; in a brief outline, one line can carry
them:

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

## Replan work that stopped converging

When rounds keep going to the same gate, instrument, or approval while the
outcome does not move, replan from the outcome rather than from the current
step. Restate what the work is for and what still stands between the current
state and a usable result. Separate the commitments made to users or the owner
from the mechanisms, gates, and evidence methods chosen to meet them: a
mechanism the outcome does not need can change, and a commitment changes only
with the person who made it.

Then choose the simplest credible route from here: cancel, reorder, or narrow
work; deliver a thin slice before a larger programme it does not depend on; or
prove the behavior another way. Effort already spent is not a reason to keep a
route. Name the simplest route even when it changes a commitment, such as an
approved gate or sequence: it then goes to the person who made it, with what it
saves and risks, and a cheaper version of the current route says why it beats
changing the commitment. Keep unmet criteria recorded as unmet rather than
relabelling them, and present the decisions the new route needs together, each
with a recommendation.

A trigger the plan sets for stalled work, such as a number of failed attempts,
returns the work to this replanning or to an independent review. It reaches the
user only when what follows changes a commitment of theirs. A limit or stop the
user set or supplied binds as written.

## Track acceptance and closeout

Map every acceptance criterion to a task contract or an explicit integration
gate with an owner. Several tasks can contribute to one outcome.

Record material deviations and their reasons in the existing plan. Preserve
unrelated unfinished work and historical evidence. Add a dated correction when
later results supersede an earlier closeout.

Distinguish implemented, verified, deployed, blocked, and deferred work. Mark
work complete only when its acceptance criteria and required checks are
satisfied. A user decision to defer work changes the recorded scope; a skipped
check is not a pass. Record completion and supporting evidence in the existing
source of truth, with a commit or artifact anchor when available. If an overview
links to detailed records, summarize completion there without duplicating the
evidence.

## Verification

- [ ] The format and detail match the size and risk of the work.
- [ ] Every requirement maps to a task or explicit gate; proposed exclusions are visible.
- [ ] New mechanisms serve a named current requirement, and the outcome was not narrowed to simplify the plan.
- [ ] Dependencies and unresolved decisions identify what they block.
- [ ] Independent work is identified where it matters, with conflicts and integration points named.
- [ ] Tasks with interpretation risk preserve contracts, boundaries, and proof.
- [ ] Verification is proportionate and does not automatically require new tests.
- [ ] Work that stopped converging was replanned from its outcome, with unmet criteria kept visible.
- [ ] A step whose result could change the design runs before proof is built around it, within authorization and off shared resources.
- [ ] Existing authorization and explicit project gates are respected.
- [ ] Substantial user involvement was surfaced before approval, with its purpose and alternatives.
- [ ] The plan has one maintained source of truth and an honest completion state.
