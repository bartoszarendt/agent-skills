---
name: code-simplification
description: Reduce demonstrated complexity while preserving intended behavior and contracts. Use when code is harder to understand or maintain than the task warrants, or when evaluating whether an abstraction or added mechanism is justified.
---

# Code Simplification

Reduce the concepts and coordination needed to make a correct change. Optimize
for clarity and maintenance cost rather than line count or the smallest diff.

## Establish a reason to change

Inspect the code, callers, tests, configuration, and relevant history. Before
proposing a simplification, identify:

- a concrete maintenance, comprehension, or operational burden;
- why the existing structure is not justified by current needs;
- a simpler alternative that preserves the required behavior;
- a benefit that exceeds implementation, verification, and regression costs.

Duplication, helper count, file size, or an unfamiliar pattern alone is not a
finding. Keep similar code separate when it represents concepts that change for
different reasons. A single implementation can justify a boundary for ownership,
isolation, compatibility, or policy.

If the evidence does not support a useful change, leave the code alone. A request
to analyze complexity does not authorize edits.

## Choose the simplest sufficient alternative

Consider removing unnecessary work, using an existing mechanism directly,
clarifying local code, or introducing a helper that represents a stable concept.
Choose by the actual burden rather than following a rigid abstraction ladder.

Check the existing stack before writing new utilities. Compare a mature
dependency with custom code by capability, maintenance, security, and operational
cost. Fewer dependencies is not sufficient justification for reimplementation.

Use names that explain the domain and actions. Prefer explicit control flow
when compact syntax hides decisions. Keep a wrapper when naming a concept or
enforcing a boundary makes callers easier to understand.

For signals and justified exceptions across different surfaces, read
[references/complexity-signals.md](references/complexity-signals.md).

## Preserve the contract

Preserve intentional inputs, outputs, side effects, ordering, and failure
semantics. Pay particular attention to:

- external interfaces and supported consumers;
- trust-boundary validation, authorization, and data invariants;
- cancellation, cleanup, reconciliation, and resource ownership;
- operator controls and diagnostic information with a real use;
- performance or compatibility constraints supported by evidence.

Distinguish these commitments from incidental structure. Existing tests can
expose regressions, but an implementation-coupled test may itself need correction.
Change a check only when its defect or an authorized behavior change is
demonstrated; preserve its valid protection.

If the proposed simplification changes a contract or removes a necessary control,
treat it as a behavior change and resolve the authorization boundary first.

## Apply coherently

Stay within the requested area. Include restructuring necessary for the solution;
report significant unrelated problems without turning the task into cleanup.

Remove confirmed unused internal code when its removal is part of the authorized
work. Check dynamic entry points and external use before concluding it is dead.

Keep changes attributable and reviewable. Separate restructuring from behavior
changes when that materially helps review or rollback. They need not be separate
commits when one coherent change is clearer, and no commit is implied.

Use automated transformations when they reduce error in repetitive edits.
Inspect their scope and result. If an attempt fails, preserve user changes and
reassess before undoing only the work from that attempt.

## Verify the result

Run existing focused checks and required gates. Add or extend tests only for a
consequential gap the change exposes. Broaden verification for affected interfaces,
persistence, concurrency, or other demonstrated risks.

Compare the result with the original burden: does a reader need fewer concepts,
lookups, or special cases to make a correct change? A longer but clearer
implementation can be the better result.

## Verification

- [ ] Each change removes a demonstrated burden at a justified cost.
- [ ] Intentional behavior and operational constraints are preserved.
- [ ] Any test changes correct a demonstrated issue without losing valid protection.
- [ ] Relevant final-state checks passed, or material gaps are reported.
- [ ] Unrelated user work and scope are preserved.
- [ ] The result is clearer without unnecessary new mechanisms.
