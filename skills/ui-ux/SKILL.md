---
name: ui-ux
description: Design and evaluate user journeys, navigation, interaction patterns, accessibility, and information presentation for web, mobile, and desktop products. Use when defining a workflow, selecting controls, investigating usability friction, or reviewing whether people can complete a task; visual restyling alone does not require a workflow redesign.
---

# UI / UX

Make the intended task understandable, operable, and recoverable. Choose patterns
from user needs, product behavior, and platform conventions rather than from a
fixed aesthetic or an industry label.

## Establish the task and evidence

Identify the user, their goal, the context of use, and the observable outcome.
Inspect the existing flow, content, components, and relevant product constraints.
Determine the supported platform and input methods from evidence; do not assume
a framework or apply mobile conventions unchanged to desktop software.

Distinguish observed friction, supplied research, and design hypotheses. A
heuristic review can identify likely problems but does not establish what real
users did or why they abandoned a flow. Do not invent research or metrics.

Clarify consequential unknowns after investigating what the project already
answers. Make routine decisions independently within the requested outcome.
A request to review or propose a flow does not authorize implementation, new
analytics, external research, or changes to product policy.

## Map the flow and its states

For the affected task, establish:

- where users start and what they need to know or provide;
- actions, choices, and dependencies along the path;
- how progress and completion are recognized;
- how back, cancel, retry, and recovery behave;
- consequential empty, loading, unavailable, permission, and failure states.

Use a short sequence or state table when useful. A single control correction
does not need a full journey map. Preserve existing vocabulary, routes, saved
work, and navigation expectations unless the requested change covers them.

Prioritize by consequence: inability to complete the task, exclusion of a
supported input method, data loss, misleading outcomes, and repeated recovery
cost generally matter more than cosmetic inconsistency. Choose priorities from
the actual flow; a chart can be critical in a data-heavy product.

## Choose controls that express the action

Use established platform controls and existing components when they express the
required behavior. Distinguish navigation, commands, selection, status, and
editable values rather than styling them as interchangeable clickable objects.

Make important actions discoverable and give related actions consistent names.
Use progressive disclosure for secondary complexity without hiding information
needed to make a decision. Choose confirmation or undo according to consequence
and reversibility; do not add a dialog to every action.

Give responsive feedback and distinguish pending, succeeded, failed, and unknown
outcomes. A timeout does not prove that a write failed. Offer retries only when
the operation's actual contract makes them safe.

For forms, navigation, asynchronous actions, and recovery patterns, read
[references/interaction-patterns.md](references/interaction-patterns.md).

## Preserve usability across access methods

Make meaningful controls reachable and understandable with the supported input
methods. Preserve keyboard focus, clear labels, reading order, system gestures,
and alternatives to precision dragging or hover-only interaction.

Choose semantics by use: an icon can be decorative, informative, or an action.
Expose its name, role, and state accordingly. Do not rely on color alone to
communicate status or on a placeholder as the only input label.

Account for text growth, translation, zoom, motion preferences, limited space,
and relevant platform safe areas. Preserve essential content and actions when
adapting density or layout. Web CSS pixels and native platform units are not
interchangeable target-size rules.

For a focused accessibility and adaptive-layout assessment, read
[references/accessibility-and-adaptation.md](references/accessibility-and-adaptation.md).
Use the current standard and platform guidance applicable to the project before
making a compliance claim; a short checklist is not a complete audit.

## Present information for decisions

Choose hierarchy, labels, grouping, and detail from what users need to compare,
find, or act on. Reuse semantic tokens and established visual conventions.
Do not generate a new palette, theme, font system, or design-system document for
a focused usability correction.

For new flows, record only the additional component behavior and shared rules
needed to keep screens consistent. Use the existing design source of truth;
page-level exceptions need a reason, not a parallel design system.

For tables, charts, filters, and compact labels, read
[references/information-and-data.md](references/information-and-data.md).
Use realistic content and label examples honestly. Do not invent endorsements,
performance claims, or production data to make a concept convincing.

## Evaluate and deliver

Walk through the primary task and the consequential interruption or failure
scenarios. If supported, inspect the rendered interface using representative
content, relevant viewport sizes, keyboard operation, and assistive technology.
Screenshots establish appearance, not successful interaction.

For a review, report the trigger, user consequence, evidence, and smallest useful
change. Separate verified defects from hypotheses needing observation. For a
proposal, state the chosen flow, key states, reasons, and unresolved decisions.

When implementation is authorized, make a coherent change and verify the
affected behavior. Reuse existing checks before adding a test; add one only for
a consequential uncovered risk. Do not expand into unrelated restyling, new
features, or backend semantics to complete a checklist.

State what was inspected, what was exercised, and what remains unverified.
Do not describe an untested design proposal as proven usable or accessible.

## Verification

- [ ] The user task, platform, and constraints are grounded in available evidence.
- [ ] Actions, states, completion, and recovery preserve the product contract.
- [ ] Controls and information support the task without unnecessary steps.
- [ ] Relevant access methods, text growth, and constrained layouts were assessed.
- [ ] Real observations, heuristic findings, and unverified proposals are distinct.
- [ ] Checks cover affected behavior without automatic test or design-system growth.
- [ ] The result stays within the authorized scope and states material evidence gaps.
