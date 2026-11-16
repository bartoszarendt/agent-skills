# Redesigns

Establish which commitments the requested redesign preserves before changing the
interface. Distinguish a visual refresh, a new visual identity, and changes to
content, navigation, or behavior.

## Inspect the current product

Review relevant pages, components, tokens, assets, interactions, and copy.
Identify public URLs, navigation paths, forms, analytics dependencies,
accessibility behavior, and meaningful search metadata where applicable.

For affected areas, keep a proportionate baseline of important content, action
destinations, fields, validation, completion, and recovery states. Include what
people must still be able to find and do, not just element names. Use existing
tests, captures, and project records when sufficient; a small refresh does not
need a new inventory file.

Record the problems the redesign should solve. Separate observed defects from
aesthetic preferences. Do not treat familiar visual patterns as defects.

If the request leaves a consequential choice unresolved, investigate available
brand guidance and examples, then ask a focused question. Honor choices already
made by the user.

## Preserve commitments

Keep supported behavior, content, identity, and compatibility that the request
does not change. A visual overhaul does not automatically authorize new routes,
different business rules, or removed functionality.

Check the consequences of changing URLs, anchors, form identifiers, navigation,
analytics events, legal text, or brand assets. Proceed when the requested scope
covers the change; otherwise resolve the material boundary first.

Preserve existing accessibility and support for the required input and viewport
range. An attractive screenshot does not justify a regression in task completion.

## Choose the extent of change

Use the smallest coherent change that solves the identified problems. Typography,
spacing, and component consistency may suffice for a refresh. Structural layout
or information architecture changes can be appropriate when authorized and
supported by evidence.

Reuse sound components and tokens. Replace them when adaptation would cost more
or preserve the defect. Do not retain weak structure solely for familiarity,
or replace working structure solely to demonstrate novelty.

## Compare the result

Compare before and after at matching viewport, content, data state, and interaction
state where possible. Check the intended improvements in hierarchy, readability,
and consistency, then ask what became harder to find, understand, or operate.
Name useful qualities that should survive further refinement.

Retained links, field names, handlers, or test hooks can reveal omissions but do
not establish functional equivalence. Exercise representative affected journeys:
follow a destination, submit through the real supported boundary, inspect the
result, and check consequential recovery. Do not make external submissions or
other shared-environment changes outside existing authorization. Use an authorized
local fixture where available and report the remaining live verification gap.

## Verification

- [ ] The redesign mode, intended improvements, and preserved commitments are clear.
- [ ] Existing important flows remain usable or changed within authorized scope.
- [ ] Affected routes, forms, analytics, and content were checked where relevant.
- [ ] Before/after comparisons use comparable conditions and preserved markup is not treated as proof of preserved behavior.
- [ ] Final rendered states and supported responsive behavior were inspected.
- [ ] Remaining verification and migration needs are stated.
