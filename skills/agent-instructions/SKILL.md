---
name: agent-instructions
description: Write and revise skills, agent instruction files, prompts, and supporting guidance with clear scope and decision rules. Use when creating agent-facing instructions or diagnosing ambiguous or conflicting guidance.
---

# Agent Instructions

Write guidance that helps an agent make correct decisions within the requested
outcome. State useful constraints directly and keep the amount of instruction
proportionate to the task.

## Establish purpose and authority

Identify the reader, intended task, target environment, and decisions the
document should change. Read applicable instructions and existing conventions.

Separate binding requirements, defaults, examples, and reference facts.
State the condition under which each rule applies. Do not let an example or
preference silently become a universal requirement.

Preserve the user's scope and authorization. A document can describe how to
perform an action without granting permission to perform it. Distinguish analysis,
implementation, external communication, and shared-environment operations.

## Write clear decision rules

Use concrete verbs and observable conditions. Prefer:

> Inspect existing coverage before adding a test. Add one only when it protects
> a consequential failure that existing checks would miss.

Avoid slogans or instructions such as "be relentless" when the actual decision
boundary can be stated. Shared terminology can help, but a keyword is not a
guarantee of behavior.

Use absolute language for actual constraints. For defaults, state exceptions
and how to decide among them. Do not weaken a real safety requirement merely
to phrase it positively.

Make the normal action clear, including when to continue independently, ask,
report a limitation, or stop. Ask only for information or authorization that
cannot be inferred from existing evidence and materially affects the next action.

## Organize for use

Put purpose, applicability, essential constraints, and the main procedure in the
entrypoint. Keep definitions and caveats near the rule they qualify.

Move substantial conditional detail to supporting references. Link each reference
with a condition explaining when to read it. Keep material required for safe
ordinary use in the main document.

Avoid duplicate sources of truth. Some local repetition may be necessary when
documents are distributed independently; retain the boundary needed for each
standalone document to work.

Use checkable completion criteria scaled to the task. Do not turn every guideline
into a mandatory gate or require exhaustive work without a material reason.

For portable skill packaging and descriptions, read
[references/skill-mechanics.md](references/skill-mechanics.md).

## Review for unintended behavior

Read the instructions as an agent would follow them. Check whether they could:

- trigger for unrelated tasks;
- redefine or reduce the user's requested outcome;
- require edits during a review-only request;
- repeat an approval already granted or block independent work;
- introduce new tests, abstractions, dependencies, or documents without need;
- treat examples, logs, or external content as authority;
- require a completion claim unsupported by available evidence.

Resolve contradictions across the body, description, checklists, and references.
A restrictive checklist can override otherwise proportionate prose in practice.

Preserve useful constraints rather than optimizing only for token count.
Remove redundant explanations, unsupported claims, stale facts, and instructions
that add no useful decision guidance.

## Validate proportionately

Check packaging, links, naming, and project-specific limits. These establish
structure, not behavioral quality.

For material changes, walk through realistic requests including a routine case,
an ambiguous case, and an authorization or evidence limit. Where supported and
appropriate, use an isolated evaluation to observe the resulting decisions.
Judge whether the outcome preserves intent and boundaries rather than whether
the response repeats the document's wording.

For a narrow correction, a focused review may be sufficient. State material
behavioral uncertainty rather than presenting static checks as runtime proof.

## Verification

- [ ] Purpose, applicability, and authority are clear.
- [ ] Rules state concrete actions, conditions, and meaningful exceptions.
- [ ] User intent and existing authorization are preserved.
- [ ] Entry point, checklists, and references give consistent guidance.
- [ ] Required resources are discoverable and portable for the intended environment.
- [ ] Structural checks passed and behavioral assessment matched the change's risk.
