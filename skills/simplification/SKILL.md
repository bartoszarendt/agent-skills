---
name: simplification
description: Judge whether scope, mechanisms, and structure are justified, and reduce what is not, in proposals, plans, technical decisions, and code while preserving required outcomes and constraints. Use when asked to simplify something or to question whether work, a dependency, a service, an abstraction, or a process step is needed; when a plan, design, or code seems more complex than its purpose warrants; or when comparing approaches that differ substantially in how much new mechanism they introduce.
---

# Simplification

Reduce the concepts, coordination, and effort needed to reach and maintain the
required outcome. Optimize for comprehension, maintenance, and operating cost
rather than line count, file count, task count, or the smallest diff. A longer
but clearer result can be the simpler one, and no change is a valid conclusion.

The same judgment applies to code and to the work around it: proposals, plans,
technical decisions, and process steps. Read the reference for the artifact at
hand:

- For code, tests, configuration, and dependencies, read
  [references/code.md](references/code.md).
- For proposals, plans, designs, technical decisions, tracking, and process
  steps, read [references/plans-and-decisions.md](references/plans-and-decisions.md).

## Establish what must remain true

Read the request, applicable instructions, the artifact, and the evidence it
depends on: for code, its callers, tests, configuration, and relevant history;
for a plan or decision, its acceptance criteria, consumers, and prior decisions.

Identify the outcome, acceptance criteria, commitments to users and consumers,
approved decisions, explicit gates, authorization, and constraints. Separate
required results from the mechanisms proposed to reach them:

- Preserve the required outcome and explicit commitments unless the user or
  responsible owner has already authorized changing them.
- A mechanism chosen only to reach the outcome is a candidate. Replacing it with
  a simpler one that meets the full outcome is a routine choice within existing
  authorization.
- Preserve a mechanism the user expressly requires or an approved decision makes
  binding, unless existing authorization covers changing it. A mechanism mentioned
  as background, a proposed option, or an artifact to simplify is not thereby
  binding. When a replacement falls outside existing authorization, present the
  alternative with its trade-off and let the user decide.

Preserve the following regardless of pressure to reduce:

- intentional inputs, outputs, side effects, ordering, and failure semantics;
- external interfaces and supported consumers;
- trust-boundary validation, authorization, and data invariants;
- error handling that prevents data loss or misleading results;
- cancellation, cleanup, reconciliation, and resource ownership;
- accessibility the outcome requires;
- operator controls and diagnostic information with a real use;
- performance or compatibility constraints supported by evidence.

## Name the burden

Before proposing a reduction, identify:

- a concrete burden, such as concepts a reader must hold, decisions, duplicated
  state, handoffs, steps, special cases, coordination, or operational effort;
- why the current or proposed structure is not justified by current needs;
- a simpler alternative that preserves what must remain true;
- a benefit that exceeds implementation, verification, migration, and
  regression costs.

Duplication, helper count, file size, task count, document length, or an
unfamiliar pattern alone is not a finding. Keep things separate when they change
for different reasons. A single implementation can justify a boundary for
ownership, isolation, compatibility, or policy.

If the evidence does not support a useful change, leave the artifact alone. A
request to analyze or evaluate complexity does not authorize edits.

## Check simpler alternatives

When choosing how to meet a need, or what could replace an existing mechanism,
look at candidates roughly in order of how much new mechanism they introduce:

1. No new work: the outcome does not require it, or existing behavior already
   provides it.
2. A mechanism already in the project: a helper, component, pattern, process,
   or record in current use.
3. A capability of the language, platform, or infrastructure already adopted,
   such as the standard library, native controls, database constraints, or
   framework features.
4. An installed dependency or established tool.
5. Direct local code or a small process change.
6. A new abstraction, dependency, service, or process.

The order says where to look, not where to stop. At each step, check whether
the candidate meets the full contract, including edge cases and the protections
above. A mechanism that resembles the need but enforces a different contract,
such as a parser used as a validator, is not suitable. A later candidate is the
better choice when it carries the contract more reliably or at lower total cost:
a mature dependency can be simpler to own than a short custom implementation
with hidden edge cases, and a small helper can be clearer than repeated compact
expressions.

Compare the realistic alternatives, usually the current state, an existing
mechanism, and the proposal. Routine choices need a sentence of rationale, not
an exhaustive option list or a scoring scheme.

## Compare total consequences

Count everything an alternative costs: implementation, verification, migration,
maintenance, operations, human effort, and the cost of reversing the choice.
Moving work from code into repeated manual steps, or from one owner onto many
callers, can increase the burden while shrinking the artifact.

When information expected later could change a choice, prefer the option that is
cheaper to reverse. Do not add abstraction or configuration solely to keep a
choice open.

## Distinguish simplification from deferral

Keep these results distinct in the artifact and in the report:

- **Complete:** an existing or simpler mechanism fully meets the requirement.
  No follow-up is implied.
- **Bounded:** the choice meets current needs under a stated assumption and has
  a known limit, such as a single lock, a linear scan, or an in-memory store.
  When later work depends on that limit, or a reader could mistake it for an
  oversight, record the limit and the observable condition that would justify
  revisiting it in the project's usual place: a code comment, the plan, or a
  decision record.
- **Deferred:** a required capability postponed with authorization from the
  user or the responsible owner. Record it as remaining scope with its
  consequence.
- **Omitted:** a required capability left out without that authorization. It
  is unfinished work, not a simplification.

## Act within scope

Stay within the requested area. Include restructuring that the solution needs;
report significant unrelated problems without turning the task into cleanup.

When changes are authorized, preserve the full outcome and the protections
above. If a reduction would change a contract, remove a necessary control, or
narrow approved scope, treat it as a behavior or scope change and resolve its
authorization first.

Remove confirmed unnecessary elements only when their removal is part of the
authorized work. Check for indirect consumers, external use, and dependents
before concluding that something is unused.

Keep changes attributable and reviewable. Separate restructuring from behavior
changes when that materially helps review or rollback; one coherent change can
be clearer, and no commit is implied. If an attempt fails, preserve user changes
and reassess before undoing only the work from that attempt.

## Verify and report

For code, run existing focused checks and required gates, and add or extend
tests only for a consequential gap the change exposes. For a plan or decision,
confirm that every acceptance criterion, approved decision, and required gate
still maps to retained work or an authorized deferral.

Compare the result with the original burden: does a reader, implementer, or
operator need fewer concepts, lookups, steps, or special cases to act correctly?

Report what was removed or replaced, what was kept and why, the material limits of
bounded choices, deferrals, and remaining costs. Describe reductions observed in
the actual artifact; a version that was never built is not a baseline for
estimated savings. A reduction in complexity does not establish correctness or
acceptance; report those from their own evidence.

## Verification

- [ ] Required outcomes, commitments, and protections were identified before reductions were proposed.
- [ ] Each change removes a demonstrated burden at a justified total cost, or no change was recommended.
- [ ] Alternatives were checked for suitability, not size alone.
- [ ] Required mechanisms and approved decisions were preserved unless their change was authorized; mentions and proposals were not treated as binding requirements.
- [ ] Complete, bounded, deferred, and omitted results are distinguished, and deferrals are recorded.
- [ ] Limits are recorded when later work depends on them or a reader could mistake them for an oversight.
- [ ] Relevant final-state checks passed, or material gaps are reported; a revised plan still maps every acceptance criterion.
- [ ] Reported reductions are observed, not estimated against an unbuilt version.
- [ ] Unrelated user work and scope are preserved.
