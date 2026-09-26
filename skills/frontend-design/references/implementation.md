# Implementation considerations

Use the existing stack, supported versions, and project conventions. Consult
current official documentation when correctness depends on framework or browser
behavior; do not adopt a package or version from an aesthetic analogy.

## Components and dependencies

Inspect existing components, tokens, and dependencies before adding another
system. Use an official design-system package when the target platform requires
it or it provides a justified capability.

Avoid mixing competing component systems without a concrete reason. A targeted
integration can be appropriate; assess accessibility, style ownership, bundle
cost, and maintenance.

Keep server and client responsibilities consistent with the framework. Isolate
interactive state where it is needed rather than moving an entire page to the
client for one effect.

## Layout and assets

Choose Grid, Flexbox, normal flow, and container constraints according to the
relationship being expressed. Test content wrapping, long labels, localization,
zoom, and empty states where they matter.

Choose viewport units based on whether the design should follow dynamic browser
chrome or keep a stable size. Verify supported devices rather than prescribing
one unit for every full-height section.

Use responsive assets and reserve layout space where dimensions are known.
Load above-the-fold and deferred assets according to measured rendering needs.
Follow the project's font hosting, licensing, and privacy constraints.

Use existing icons and vectors when suitable. Custom vector work is appropriate
when required by the product and maintainable within its asset system.

## Interaction and motion

Prefer native semantics for links, buttons, forms, disclosure, and navigation.
Verify keyboard behavior and focus transitions when state or route changes.

Choose CSS or an existing animation mechanism before adding a library.
Use transforms and opacity where they achieve the effect efficiently, but do not
turn that preference into a ban on necessary layout transitions.

For scrolling or pointer effects, avoid unnecessary rendering on every event.
Use an appropriate browser or framework mechanism and measure when performance
is uncertain. Account for cleanup, resizing, dynamic content, and reduced motion.

If a motion effect cannot be completed in scope, preserve a usable static state
and report the omitted behavior. Do not silently drop motion that is a required
part of the requested outcome.

## Themes and states

Use the project's semantic color and theme strategy. Verify each supported theme;
do not introduce an additional scheme or toggle without a requirement or benefit
that justifies its cost.

Implement loading, error, empty, disabled, and success states relevant to the
flow. Preserve authorization and data correctness behind those states.

## Runtime checks

Inspect the final rendering where tools are available. Check representative
widths, overflow, focus visibility, label association, contrast, reduced motion,
and important interactions.

Use existing static, component, and browser checks according to risk. Assess
performance against the product's targets with representative builds and
measurements; a hardcoded universal budget is not evidence of suitability.
