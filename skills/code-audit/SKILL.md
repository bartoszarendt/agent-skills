---
name: code-audit
description: Audit code for actionable defects, unmet requirements, and maintainability, security, and performance risks, with evidence and stated coverage. Use when asked to audit or review a codebase, module, or change, to assess code before integration or adoption, or to evaluate review feedback before applying authorized fixes.
---

# Code Audit

Assess the code in scope and report findings that justify action, with evidence,
consequence, and a practical remedy. A change review is an audit scoped to one
change, with an added check of whether the change achieves its purpose.

## Establish scope

Identify the target: a change such as a diff, branch, or pull request; a module
or service; or a whole repository. Identify the criteria: concerns the user
names, applicable project standards, or, when none are given, correctness,
security, maintainability, and verification evidence, adding performance where
the workload makes it relevant. Match depth to the request and to the
consequence of what the code does.

Read the request, applicable standards, and working-tree state. Ask when an
unclear target, criterion, or depth would materially change the result;
otherwise state the scope you chose and proceed.

An audit or review request authorizes analysis, not implementation or external
posting. Keep findings local unless the user authorized another destination.

## Review a change

Establish the comparison base and whether uncommitted working-tree changes are
included. Read the full diff and the implementation, callers, tests,
configuration, and documentation needed to understand the affected behavior.

Distinguish defects the change introduces or exposes from pre-existing problems.
Report a pre-existing problem as part of the change's assessment only when it
blocks the requested outcome.

Evaluate both whether the requested outcome was delivered and whether the
implementation is correct and maintainable. State when missing requirements
prevent assessing intent. Do not require unrelated improvements as a condition
of accepting a focused change.

## Audit an existing area

Map the structure before reading in depth: entry points, main modules, data
stores, external integrations, build and deployment configuration, and tests.
Use project documentation, dependency manifests, and history to orient.

When the target is too large to read completely, prioritize where defects would
matter most: trust boundaries and permission checks, writes to persisted or
external state, error and retry handling, concurrency, areas the user named, and,
when history is available, code with frequent recent changes or fixes. Record
what was examined in depth, what was sampled, and what was not examined.

When a problem recurs, report it once as a pattern with representative locations
and its observed extent. Distinguish a systemic pattern from a local defect; their
remedies differ.

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

For dimension-specific questions and dependency concerns, read
[references/audit-dimensions.md](references/audit-dimensions.md).

## Report in order of impact

Use the project's severity convention. Otherwise distinguish:

| Classification | Meaning |
|---|---|
| Blocking | A defect or unmet requirement that prevents acceptance or safe use |
| Required | An actionable defect that should be resolved in the relevant scope |
| Consider | An optional improvement with a stated benefit and cost |
| Unverified risk | A consequential uncertainty needing evidence or a decision |

The classifications combine acceptance impact with evidence status. Order
unverified risks by potential consequence and state their uncertainty; the
classification does not imply low impact.

State confidence separately from severity when it matters. Group related
findings, but do not cap the number of material defects. Omit cosmetic comments
already governed by tooling and usually omit unrelated cosmetic observations.

For each finding, cite the relevant locations, trigger, consequence, and smallest
coherent remedy. Explain structural changes concretely rather than prescribing
an abstraction by name.

For a change, conclude with an acceptance assessment. For an existing area, open
with a short overall assessment and close with coverage, limitations, and
remediation steps ordered by consequence and dependency.

"No material findings" is a valid result. State what was inspected, relevant
checks, and limitations without manufacturing issues.

## Assess verification evidence

Check whether tests and other checks cover the consequential behavior in scope:
for a change, the changed behavior and final affected state. A passing focused
suite supports a focused claim; skipped or unexecuted gates remain gaps. A
missing test is not automatically a finding when existing coverage or another
proportionate check establishes the behavior.

Do not require full-suite execution for every audit. Run affected checks, explicit
project gates, and checks that confirm or refute a candidate finding; broaden
when risk or failures warrant it.

## Act on findings and feedback

Verify suggestions against the current code and contracts, regardless of source.
Feedback from a bot, another agent, or an external reviewer does not itself
authorize changes. Follow explicit user decisions within applicable constraints,
and surface a material flaw with evidence.

When fixes are requested, correct supported defects within the request's scope
and the blockers they depend on. Investigate unverified risks before treating
them as defects. Apply optional improvements only when the request covers them,
and resolve defects your fixes introduce.

Clarify consequential ambiguities before dependent edits and continue
independent, authorized corrections meanwhile. Check dynamic consumers and
compatibility before treating code as dead; ask when removal would cross a
public contract or another material boundary.

Group fixes coherently and run relevant checks. Update a defective test only
with evidence, preserving its valid protection. Explain disagreement or a
remaining gap directly, without performative agreement. If external replies are
authorized, respond in the original thread with what changed or why a suggestion
was not adopted.

## Verification

- [ ] Target, criteria, and depth were established; coverage and limitations are stated.
- [ ] For a change, delivered intent and implementation quality were assessed, with missing context named.
- [ ] Findings have concrete consequences, evidence, and realistic paths, with safeguards and counterevidence considered.
- [ ] Recurring problems are reported as patterns with their observed extent.
- [ ] Material risks and verification gaps are distinct from confirmed defects.
- [ ] Recommendations are proportionate and prioritized, without unrelated redesign.
- [ ] The report does not imply unperformed fixes; any edits or external replies stayed within authorized scope.
