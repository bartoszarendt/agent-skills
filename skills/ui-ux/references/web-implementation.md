# Web implementation

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

Map a visual proposal onto the project's existing semantic tokens and component
variants. Check where a token is consumed before changing it globally. Scope a
page-specific treatment when it should not alter shared controls; preserve existing
theme selectors and CSS conventions rather than creating a competing token set.

## Layout and assets

Choose Grid, Flexbox, normal flow, and container constraints according to the
relationship being expressed. Test content wrapping, long labels, localization,
zoom, and empty states where they matter.

Choose adaptation points where content or controls need them. Check intermediate
widths around those changes, not only a desktop and phone screenshot. Recompose
columns into a meaningful reading order; do not hide essential evidence or actions
to make the smaller layout fit. Keep intentional wide tables operable instead
of shrinking their text beyond useful readability.

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

On touch devices, apply hover styles only where the primary pointer can hover,
for example under `@media (hover: hover)`, so a tap does not leave a hover
state behind, and keep hover-revealed actions reachable without hover. Give
text fields at least a 16 CSS pixel font size where iOS Safari would otherwise
zoom on focus. Keep a control mounted across layout changes while it stays
visible, so focus and unsent input survive a resize. Do not raise the
on-screen keyboard automatically unless typing is the intended next step.
Choose layout from media features and available space, not from a parsed user
agent; media features do not detect a physical keyboard.

Choose CSS or an existing animation mechanism before adding a library.
Use transforms and opacity where they achieve the effect efficiently, but do not
turn that preference into a ban on necessary layout transitions.

Ask what would be lost if the change happened instantly. Motion can explain a
relationship or acknowledge an action; decoration alone does not justify delaying
the next input.

For scrolling or pointer effects, avoid unnecessary rendering on every event.
Use an appropriate browser or framework mechanism and measure when performance
is uncertain. Account for cleanup, resizing, dynamic content, and reduced motion.

Treat scroll choreography as enhancement to an already readable sequence. Preserve
the information and a useful static order when the effect or its required browser
capability is unavailable. For a pinned explanation beside changing evidence,
check the unpinned reading order, keyboard navigation, and short windows before
adding further transitions. Do not simulate browser scrolling to force a sequence.

If a motion effect cannot be completed in scope, preserve a usable static state
and report the omitted behavior. Do not silently drop motion that is a required
part of the requested outcome.

## Themes and states

Use the project's semantic color and theme strategy. Verify each supported theme;
do not introduce an additional scheme or toggle without a requirement or benefit
that justifies its cost.

Implement loading, error, empty, disabled, and success states relevant to the
flow. Preserve authorization and data correctness behind those states.

Keep the control's purpose recognizable during those changes. For example, reserve
the space needed for a save action's progress feedback instead of replacing it
with a narrower icon that moves adjacent controls. Preserve room for errors without
clipping translations. Visual loading or success styling must follow the real
operation, including an unconfirmed outcome.

## Runtime checks

Inspect the final rendering where tools are available. Check representative
widths, overflow, focus visibility, label association, contrast, reduced motion,
and important interactions.

Inspect supported motion both in its ordinary
mode and with reduced motion when relevant; a capture with motion disabled alone
does not establish that the animation works. Exercise controls whose behavior
changed, including relevant failure and keyboard paths. Finding a focus selector,
request call, or media query in source does not establish that behavior ran.

Use existing static, component, and browser checks according to risk. Assess
performance against the product's targets with representative builds and
measurements; a hardcoded universal budget is not evidence of suitability.
