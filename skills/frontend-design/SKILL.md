---
name: frontend-design
description: Create and implement a coherent visual direction for web pages, components, and application screens. Use for visual composition, typography, color, assets, styling, responsive rendering, or a visual redesign; a flow-only usability assessment does not require restyling.
---

# Frontend Design

Make visual and interaction choices that serve the product, audience, and task.
Preserve established behavior and identity unless the requested scope changes them.

Focus on visual composition and rendered implementation. Use the established
user flow as a constraint; do not turn a styling task into a navigation or
workflow redesign. Accessibility and interaction checks remain part of delivering
working visual changes.

## Read the brief and existing interface

Identify the main user action, content, audience, constraints, and supplied
references. Inspect the existing components, tokens, assets, and supported states
before introducing a new system.

Distinguish a new interface, a brand-preserving update, and a visual overhaul.
For changes to an existing interface, read
[references/redesign.md](references/redesign.md).

State consequential assumptions briefly. Ask when missing product context or a
material choice would change the outcome; otherwise choose a supported direction
and proceed within authorization. Do not invent a client's history or preferences.

## Choose a coherent direction

Define enough of the visual system to guide the work:

- typography roles, scale, and readable measure;
- semantic colors, contrast, and interaction states;
- spacing, layout, alignment, and responsive behavior;
- shape and icon conventions;
- motion only where it contributes to feedback or understanding.

Reuse the project's design system when it meets the need. Consider an official
system when the actual platform or product requires one, rather than installing
a package because the brief resembles its aesthetic.

Make deliberate choices grounded in content and brand. Familiar patterns are
appropriate when they support the task. Distinctiveness is not a reason to
replace clear navigation or introduce decorative complexity.

Use a short token list or sketch when useful. A small component change may only
need the existing tokens and a stated adjustment.

## Build the complete relevant flow

Implement the requested behavior, including consequential loading, empty, error,
disabled, and success states. Preserve existing interactions and avoid presenting
a static mockup as a working feature.

Design for the supported viewport and input range. Check keyboard access, visible
focus, meaningful labels, semantics, contrast, and reduced-motion behavior.
Use current applicable accessibility requirements and project standards.

Choose layouts from content needs rather than numerical quotas. Cards, tables,
lists, centered headings, repeated sections, and visual emphasis are options.
Use each where it clarifies relationships or supports scanning.

Animate when feedback, hierarchy, or state change benefits. Prefer inexpensive
properties when suitable, measure problematic effects, and clean up observers
and animation resources. Respect reduced-motion preferences.

Implement color schemes required by the brief or existing product. Do not add a
second theme solely because the interface is consumer-facing.

For stack-specific considerations, read
[references/implementation.md](references/implementation.md). For marketing
surfaces, read [references/landing-pages.md](references/landing-pages.md).

## Use truthful assets and copy

Reuse suitable supplied assets before creating new ones. Use generated imagery
when it serves the brief and tools are available; availability alone is not a
reason to generate an image. Match icon and asset choices to the existing system.

Label temporary imagery and sample content. Do not invent endorsements, customer
logos, precise claims, or screenshots presented as a real product. A clearly
identified mockup is appropriate when that is the requested deliverable.

Write from the user's perspective. Name actions consistently and say what happens
next. Errors should identify the problem and an available recovery action.
Avoid exposing implementation details unless they help a meaningful decision.

Use plain, concise language and the product's voice. Choose punctuation,
capitalization, and label length for clarity and established conventions, rather
than treating a particular word or punctuation mark as proof of generated text.

## Verify the result

Inspect the rendered final interface where the environment supports it. Check
representative widths, required themes, keyboard behavior, and important states.
Use screenshots when they help compare the result with the brief; do not treat
a screenshot as proof of interaction correctness.

Run relevant existing checks and required project gates. Add automated tests only
for consequential uncovered behavior. If browser or accessibility verification
is unavailable, state that limitation and the checks actually completed.

Review visible copy and assets for accuracy. Stop when the requested result is
usable and coherent; do not expand into an unrelated rebrand or component rewrite.

## Verification

- [ ] The direction follows the brief, existing product, and user task.
- [ ] Tokens, assets, and components form a consistent system.
- [ ] Required interactions and consequential states work.
- [ ] Responsive behavior and applicable accessibility requirements were checked.
- [ ] Copy and assets are truthful, with temporary content identified.
- [ ] Final rendered behavior was inspected where available; remaining gaps are explicit.
- [ ] Scope and existing compatibility commitments are preserved.
