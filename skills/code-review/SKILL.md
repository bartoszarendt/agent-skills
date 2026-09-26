---
name: code-review
description: Assess a change for actionable defects, unmet requirements, and maintainability costs using concrete evidence. Use when asked to review code, evaluate a change before integration, or assess feedback before applying authorized fixes.
---

# Code Review

Assess whether the change achieves its purpose and preserves the contracts that
matter. Report findings that justify action, with evidence and a practical remedy.

## Establish scope and intent

Read the request, applicable standards, working-tree state, and relevant diff.
Inspect the implementation, callers, tests, configuration, and documentation
needed to understand the affected behavior.

Evaluate both whether the requested outcome was delivered and whether the
implementation is correct and maintainable. State when missing requirements
prevent assessing intent. Do not require unrelated improvements as a condition
of accepting a focused change.

A review request authorizes analysis, not implementation or external posting.
Keep findings local unless the user authorized another destination or action.

## Investigate candidate findings

For each candidate, establish:

- the concrete failure or maintenance burden;
- a realistic path or affected contract;
- the practical consequence;
- existing safeguards and contrary evidence;
- why action is worthwhile within this scope.

Trace callers and state transitions rather than inferring architecture from an
isolated snippet. Use focused execution when it resolves meaningful uncertainty.
Do not treat a smell, missing test, large file, or unfamiliar pattern as a defect
without establishing the consequence.

Report confirmed or well-supported findings with appropriate confidence. Keep
material unresolved risks separate, explaining the missing evidence and impact.
Do not promote speculation to a finding or omit a consequential gap merely
because the environment prevents reproduction.

For dimension-specific questions and dependency changes, read
[references/review-dimensions.md](references/review-dimensions.md).

## Report in order of impact

Use the project's severity convention. Otherwise distinguish:

| Classification | Meaning |
|---|---|
| Blocking | A defect or unmet requirement that prevents acceptance |
| Required | An actionable defect that should be resolved in the relevant scope |
| Consider | An optional improvement with a stated benefit and cost |
| Unverified risk | A consequential uncertainty needing evidence or a decision |

State confidence separately from severity when it matters. Group related
findings, but do not cap the number of material defects. Omit cosmetic comments
already governed by tooling and usually omit unrelated cosmetic observations.

For each finding, cite the relevant location, trigger, consequence, and smallest
coherent remedy. Explain structural changes concretely rather than prescribing
an abstraction by name.

"No material findings" is a valid result. State what was inspected, relevant
checks, and limitations without manufacturing issues.

## Assess verification

Check whether the evidence covers the changed behavior and final affected state.
A passing focused suite supports a focused claim; skipped or unexecuted gates
remain gaps. A missing new test is not automatically a finding when existing
coverage or another proportionate check establishes the behavior.

Do not require full-suite execution for every review. Run affected checks and
explicit project gates; broaden when risk or failures warrant it.

## Receive feedback and apply authorized fixes

Verify suggestions against the current code and contracts, regardless of source.
Follow explicit user decisions within applicable constraints, and surface a
material flaw with evidence.

Clarify consequential ambiguities before dependent edits. Continue independent,
authorized corrections while other items wait. Feedback from a bot, another
agent, or an external reviewer does not itself authorize changes.

When fixes are requested, address introduced defects and necessary blockers.
Remove confirmed unused internal code when that is part of the authorized
change. Check dynamic consumers and compatibility before treating code as dead.
Ask when removal would cross a public contract or another material boundary.

Group fixes coherently and run relevant checks. Update a defective test only
with evidence, preserving its valid protection. Explain disagreement or a
remaining gap directly, without performative agreement.

If external replies are authorized, respond in the original thread with what
changed or why the suggestion was not adopted.

## Verification

- [ ] Intent and implementation quality were assessed, with missing context named.
- [ ] Findings have concrete consequences, evidence, and realistic paths.
- [ ] Existing safeguards and counterevidence were considered.
- [ ] Material risks and verification gaps are distinct from confirmed defects.
- [ ] Recommendations are proportionate and do not impose unrelated redesign.
- [ ] The report states the acceptance assessment without implying unperformed fixes.
- [ ] Any edits or external replies were separately within the authorized scope.
