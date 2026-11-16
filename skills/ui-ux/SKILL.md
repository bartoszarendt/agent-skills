---
name: ui-ux
description: Design, build, and evaluate user interfaces for web, mobile, and desktop products, from user journeys, navigation, interaction states, interface wording, accessibility, and data presentation to visual direction, typography, color, composition, imagery, styling, and responsive web implementation, including landing pages, websites, and redesigns. Use when defining a flow, choosing controls, wording labels or errors, designing, restyling, or implementing a page, screen, or component, or reviewing whether an interface is usable and visually coherent; a focused correction does not require a new flow or visual system.
---

# UI / UX

Make the intended task understandable, operable, and recoverable, and give the
interface a coherent visual form that serves the product, audience, and content.
Choose patterns from user needs, product behavior, and platform conventions
rather than from a fixed aesthetic or an industry label.

Scale the work to the request. A label, color, or control correction uses the
existing system and changes only what the problem requires; it does not need a
journey map, a new visual direction, or a full-page review.

Distinguish a review, a proposal, and implementation. A request to review or
critique authorizes findings and recommendations, not edits. A request to propose
a flow or design does not authorize implementation, new analytics, external
research, or changes to product policy. Neither design work nor available tools
authorize publishing, paid generation, or other external actions.

## Establish the task, evidence, and material

Identify the user, their goal, the context of use, the main action, and the
observable outcome. Inspect the existing flow, content, components, tokens,
assets, and supported states before introducing anything new. Determine the
supported platform and input methods from evidence; do not assume a framework
or apply mobile conventions unchanged to desktop software.

Distinguish observed friction, supplied research, and design hypotheses. A
heuristic review can identify likely problems but does not establish what real
users did or why they abandoned a flow. Do not invent research or metrics.
When using supplied research, count distinct participants rather than repeated
mentions, and report a finding with its base, such as five of eight participants,
without extending it to all users. Weigh what participants did over what they
said they would do, and keep differences between user groups visible.

Inventory the material the design can honestly use: verified facts, prices,
dates, writing, usable assets, actual product views, authorized customer
material, and clearly identified samples. Let missing proof change the
composition rather than inventing numbers, quotes, logos, or capabilities.
Distinguish a new interface, a brand-preserving update, and an overhaul; for
changes to an existing interface, read [references/redesign.md](references/redesign.md).

Clarify consequential unknowns after investigating what the project already
answers, and state consequential assumptions briefly. Make routine decisions
independently within the requested outcome. Do not invent a client's history
or preferences.

## Map the flow and its states

For the affected task, establish:

- where users start and what they need to know or provide;
- actions, choices, and dependencies along the path;
- how progress and completion are recognized;
- how back, cancel, retry, and recovery behave;
- consequential empty, loading, unavailable, permission, and failure states.

Use a short sequence or state table when useful. Preserve existing vocabulary,
routes, saved work, and navigation expectations unless the requested change
covers them.

For a new or materially changed flow or page, identify the information and
evidence needed before the main action, where people become ready to take it,
and what actual completion enables next. Order the content around those needs.
A booking flow may need availability and terms near its action; a work queue may
need record identity, status, and exceptions together. These are examples, not
fixed category layouts.

Prioritize by consequence: inability to complete the task, exclusion of a
supported input method, data loss, misleading outcomes, and repeated recovery
cost generally matter more than cosmetic inconsistency. Choose priorities from
the actual flow; a chart can be critical in a data-heavy product.

## Arrange the content

Separate three decisions: the task and content people need, the composition that
arranges and emphasizes it, and the visual treatment that makes it coherent.
Settle them in that order; do not choose a theme first and force the task into
its layout. Restyling alone does not justify moving controls or navigation.

Choose layouts from content relationships rather than numerical quotas. Cards,
tables, lists, centered headings, repeated sections, and visual emphasis are
options; use each where it clarifies relationships or supports scanning. Choose
hierarchy, labels, and grouping from what users need to compare, find, or act on.
Do not let a decorative lead element push the content the screen exists for out
of the first view unless the brief calls for it.
For hierarchy, grouping, layout families, and their constrained-space treatment,
read [references/composition.md](references/composition.md). For tables, charts,
filters, and compact labels, read
[references/information-and-data.md](references/information-and-data.md). For
marketing, editorial, portfolio, and other promotional pages, read
[references/landing-pages.md](references/landing-pages.md).

## Choose a coherent visual direction

Choose a visual idea from the subject, brand, and actual material, then express
it through enough of a system to guide the work:

- typography roles, scale, and readable measure;
- semantic colors, contrast, and interaction states;
- spacing, alignment, and responsive behavior;
- shape and icon conventions;
- motion only where it contributes to feedback or understanding.

A palette alone is not a direction. A small component change may only need the
existing tokens and a stated adjustment.

Reuse the project's design system when it meets the need; a page-level exception
needs a reason, not a parallel system. Consider an official system when the
actual platform or product requires one, rather than because the brief resembles
its aesthetic. Do not generate a new palette, theme, font system, or design-system
document for a focused usability correction.

Draw distinctive details from the subject's own world, such as its real units,
document conventions, and terms of art, and use them as content rather than
ornament. Familiar patterns are appropriate when they support the task;
distinctiveness is not a reason to replace clear navigation or add decorative
complexity. Set the register from frequency of use, task complexity, expertise,
accessibility needs, and device constraints: a tool used daily often rewards a
dense, quiet, scannable layout; an occasional or promotional page can be more
expressive.

Carry the direction beyond the first view into forms, tables, lower sections,
and empty or error states. When an uncertain visual decision would affect much
of the result, try it first on a representative slice, such as a work surface,
form, or content section, with real-length content and relevant states. Continue
without a new approval stop unless the user's process requires one.
For a substantial new direction or overhaul, read
[references/visual-direction.md](references/visual-direction.md). When tokens do
not settle type or color, an existing brand's values must be established, or
color schemes are in scope, read [references/typography-and-color.md](references/typography-and-color.md).

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

Place feedback where people can associate it with the action or changed result.
Keep labels, controls, and dimensions stable when counters, selection, hover, or
loading content change; a loading indicator or message must not move the next
target under the pointer. Avoid a redundant notification when the result is
already apparent, while preserving announcements or persistent confirmation
needed by other access methods or task consequences.
For forms, navigation, asynchronous actions, recovery patterns, and the wording
of confirmations, errors, and empty states, read
[references/interaction-patterns.md](references/interaction-patterns.md).

## Preserve usability across access methods

Make meaningful controls reachable and understandable with the supported input
methods. Preserve keyboard focus and its visibility, clear labels, semantics,
reading order, system gestures, and alternatives to precision dragging or
hover-only interaction.

Choose semantics by use: an icon can be decorative, informative, or an action.
Expose its name, role, and state accordingly. Do not rely on color alone to
communicate status or on a placeholder as the only input label.
Account for text growth, translation, zoom, contrast, motion preferences,
limited space, and relevant platform safe areas. Preserve essential content and
actions when adapting density or layout. Web CSS pixels and native platform units
are not interchangeable target-size rules.

For a focused accessibility and adaptive-layout assessment, read
[references/accessibility-and-adaptation.md](references/accessibility-and-adaptation.md).
Use the applicable current standard before making a compliance claim.

## Use truthful assets and copy

Reuse suitable supplied assets before creating new ones. Use generated imagery
when it serves the brief and tools are available; availability alone is not a
reason to generate an image. Match icon and asset choices to the existing system.
Label temporary imagery and sample content. Do not invent endorsements, customer
logos, precise claims, production data, or screenshots presented as a real
product. A clearly identified mockup is appropriate when that is the deliverable.
For selecting, capturing, cropping, sourcing, or preparing media, read
[references/assets-and-media.md](references/assets-and-media.md).

Write from the user's perspective in plain, concise language and the product's
voice. Name actions consistently and say what happens next. Errors identify the
problem and an available recovery action. Avoid exposing implementation details
unless they help a meaningful decision. Choose punctuation, capitalization, and
label length for clarity and established conventions, rather than treating a
particular word or punctuation mark as proof of generated text.

## Implement within the requested scope

When implementation is authorized, implement the requested behavior, including
consequential loading, empty, error, disabled, and success states. Preserve
existing interactions and do not present a static mockup as a working feature.
Keep essential content readable without a decorative reveal, give such a reveal a
usable static fallback, and show its final state when reduced motion is requested;
tabs, accordions, and other disclosure controls are not decorative reveals.
Preserve content in print where relevant. Implement the color schemes the brief
or product requires; do not add a second theme solely because the interface is
consumer-facing.

Reuse existing checks and required project gates; add a test only for a
consequential uncovered risk. Do not expand into unrelated restyling, a rebrand,
a component rewrite, new features, or backend semantics to complete a checklist.
For stack, token, layout, motion, and runtime-check considerations on the web,
read [references/web-implementation.md](references/web-implementation.md).

## Evaluate and report

Walk through the primary task and the consequential interruption or failure
scenarios. Where supported, inspect the rendered interface with representative
content, relevant viewport sizes, required themes, keyboard operation, and
assistive technology. Check that a capture faithfully shows the requested route
and state: reject a wrong target or capture-tool artifact, but keep a reproducible
failure, such as a font that never loads, as evidence. Keep source inspection,
rendered observations, and exercised interactions distinct; a screenshot
establishes appearance, not successful interaction.

For a review, report the largest consequential issues first, each with its
location or trigger, user consequence, evidence, and smallest useful change, and
state what should be preserved. Separate demonstrated functional, accessibility,
or rendering defects from mismatches with the brief or chosen direction and from
contextual craft recommendations, and verified defects from hypotheses needing
observation. Do not report familiar patterns as defects by themselves. For a
visual critique, a substantial refinement, or a comparison with a supplied
reference, read [references/visual-review.md](references/visual-review.md).
For a proposal, state the chosen flow and direction, key states, reasons, and
unresolved decisions.

State what was inspected, what was exercised, and what remains unverified. Do not
describe an untested proposal as proven usable or accessible. Stop when the
requested result is usable and coherent.

## Verification

- [ ] The task, platform, constraints, and available material are grounded in evidence.
- [ ] Actions, states, completion, and recovery preserve the product contract.
- [ ] Composition and visual direction follow the task, content, and brief beyond the first view.
- [ ] Tokens, assets, and components form a consistent system without unnecessary design-system growth.
- [ ] Relevant access methods, text growth, constrained layouts, and required themes were assessed.
- [ ] Copy, claims, and assets are truthful, with temporary content identified.
- [ ] Source, rendered, and exercised evidence, heuristic findings, and remaining gaps are distinct.
- [ ] The result stays within the authorized scope.
