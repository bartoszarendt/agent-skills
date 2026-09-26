---
name: testing-and-verification
description: Choose and maintain tests that protect consequential behavior with proportionate verification. Use when assessing coverage, adding or repairing tests, selecting evidence for a change, or applying a test-first workflow.
---

# Testing and Verification

Choose checks that establish the required behavior at a reasonable maintenance
cost. Test count and coverage percentages are diagnostics, not completion goals.
Follow explicit user and project test requirements, including a required
test-first method. Explain a material trade-off rather than silently omitting it.

## Decide whether a test is needed

Read the affected contract, implementation, and existing coverage first. Identify
what can go wrong, how it can occur, and why the consequence matters.

Before adding a test, name the consequential failure existing checks would miss.
If you cannot name it, do not add the test. Prefer running, extending, or
correcting an existing case over overlapping coverage.

Add protection for a likely regression, important business rule, public
contract, security boundary, data invariant, or realistic concurrency failure.
Configuration-driven behavior may warrant a test when its consequences matter.

For low-risk prose, static content, or mechanical changes, inspection, a build,
or a focused manual check may be sufficient. Record the evidence needed to
support the result; do not create test infrastructure to demonstrate effort.

## Discover how checks run

Inspect project commands, checked-in wrappers, neighboring tests, and CI
configuration. Identify the cheapest relevant checks and required gates.
Do not assume a package manager, runner, or full-suite command.

Confirm that the runner discovers the intended cases and that assertions execute.
Zero tests, unexpected skips, missing services, and incomplete runs do not
establish success.

## Select the right level

Use the lowest-cost layer that reliably observes the contract.

- Test pure behavior directly when external wiring is irrelevant.
- Use integration or runtime checks when the risk concerns persistence,
  serialization, permissions, browser behavior, or service compatibility.
- Cover materially different risks at different layers. Do not repeat the same
  permutations across layers without distinct protection.
- Use representative cases instead of large parameter combinations that exercise
  the same behavior.

Test observable outcomes and stable contracts. Exact text, call counts, database
state, or snapshots can be appropriate when that is the contract at risk.
Avoid freezing private structure merely because it is convenient to assert.

## Apply test-first work where useful

When a new or extended test is justified and the defect can be reproduced:

1. Express the relevant behavior and expected result.
2. Run the case against the unfixed behavior where practical.
3. Confirm that it fails for the predicted reason, not a broken fixture or import.
4. Implement the coherent fix and run the focused check.
5. Run other affected checks and required gates.

A test that passes immediately may cover existing behavior. Investigate whether
it adds needed protection; do not modify it merely to force a failure.

For tests added after implementation, establish sensitivity against a known-bad
version or one bounded mutation in a scratch copy when practical and worthwhile.
Never discard user work to manufacture a failing run. If sensitivity remains
unproven, say so when that limits the conclusion.

Use the test-first sequence as a method, not as a reason to delete valid work,
block diagnosis, or require a new test for every edit.

## Keep tests useful

Derive expectations independently from the production logic. Use a hand-checked
example, a specification, or an independent oracle rather than invoking the same
helper on both sides of the assertion.

Keep related assertions together when they establish one outcome, including
absence of side effects on failure. Split cases when that improves diagnosis of
distinct risks, not because the name contains a conjunction.

Prefer real components when they are affordable and deterministic. Use fakes,
stubs, or mocks at meaningful boundaries when they isolate the risk honestly.
Internal substitution can be justified for expensive or uncontrollable behavior;
it does not by itself establish an architectural defect.

Assert interactions when the interaction is the observable contract, such as
one external submission with the required payload. Do not present mocked
transport evidence as proof of a live integration.

Keep fixtures and helpers no more elaborate than the behavior requires. Prefer
readable setup; consolidate directly affected redundancy when protection remains
clear. Do not expand into unrelated suite cleanup.

For async behavior, flakes, negative cases, snapshots, and test discovery, read
[references/test-quality.md](references/test-quality.md).

## Evaluate failures and coverage

Determine whether a failure comes from the change, an existing defect, the test,
or the environment. Update expectations only for an intentional contract change
or a demonstrated defect in the check, preserving valid protection.

Do not hide failures, loosen valid assertions, or disable checks to reach green.
Use mutation or coverage results to investigate meaningful gaps rather than
requiring protection for every branch or constant.

Run focused checks first. Expand for demonstrated risk or project requirements.
Repeat after edits that could invalidate evidence, not simply for reassurance.

## Verification

- [ ] Each added test protects a named consequential risk absent from existing coverage.
- [ ] The selected layer exercises the behavior being claimed.
- [ ] Expectations are independent and valid protection was preserved.
- [ ] Cases execute, handle async work, and clean up owned resources.
- [ ] Relevant final-state checks and required gates ran, or gaps are explicit.
- [ ] The report distinguishes passing, failing, skipped, and unexecuted checks.
