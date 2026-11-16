# Typography and color

Use this reference when choosing or substantially changing type or color, when
content exposes weaknesses in the existing system, or when implementing required
color schemes. Preserve established tokens for a focused correction when they
already express the needed hierarchy and states.

## Establish brand values from their sources

When the work must match an existing brand, establish its typefaces and colors
from evidence. Consult, as available: guidance and assets the user supplied; the
project's tokens, styles, and asset files; the brand's official published
resources, when web access is available and permitted; and the rendered product
where implemented values matter. Do not reconstruct a real brand's palette or
typefaces from memory, a resemblance, or the most frequent colors in a screenshot.

Keep each value's provenance apparent where it matters: specified by brand
guidance, implemented in the project, observed in rendering, or inferred. Do not
present an inferred value as the brand's specification. When sources disagree,
such as guidance and the shipped product, preserve the implemented values for a
focused change and report the discrepancy; resolve it only within the requested
scope. Published brand material does not grant rights to fonts or marks beyond
its terms. If no authoritative source is available, use the project's implemented
values or state the missing specification.

## Choose type on actual content

Set representative headings, paragraphs, labels, figures, and controls in the
candidate face. Include the longest important strings, the languages the product
supports, and characters people must distinguish. Judge the rendered content at
its intended size; a font's category, name, or reputation cannot establish its fit.

Choose roles before adding families or sizes. Distinguish the main message,
section headings, item titles, running text, supporting labels, and comparable
figures where the interface needs them. Use size, weight, spacing, and placement
to express their relationships. A single family can provide enough range; add
another when it contributes a clear role and its loading cost is justified.

Match the amount of differentiation to the task. A dense tool may need quieter
headings and stronger row alignment than a promotional page. Preserve readable
supporting text instead of shrinking it until a preferred composition fits.
Choose line height and measure together with size, face, language, and content;
inspect the actual reading experience rather than imposing a universal scale.

## Shape headings, prose, and figures

Let headings wrap at meaningful boundaries across supported widths. Use a
deliberate line break only when it holds with the actual content, narrower layouts,
and relevant translations. Text balancing can help where supported; retain readable
wrapping without it. Do not force a line count by dropping useful words or hiding
overflow.

Keep running text in a comfortable measure and provide enough line separation
to track it. Increase distinction through spacing or weight when more colors or
type sizes would fragment the hierarchy. Inspect emphasized words in context;
emphasis should communicate meaning and preserve contrast.

Align comparable values and retain their units, signs, and precision. Consider
tabular numerals when changing digit widths would hinder comparison or move
content. Use a monospaced face when code, alignment, or the product's established
register needs it; do not turn every small label into technical notation.
Use appropriate locale formatting and keep a value with its unit when practical
without preventing necessary wrapping in constrained layouts.

## Load fonts without making content fragile

Check the project's licensing, hosting, privacy, and browser-support constraints.
Use suitable supplied or installed fonts before adding a remote dependency.
Load the styles, weights, character coverage, and formats the interface actually
uses. A variable font may reduce requests, but compare the actual files and needed
range rather than assuming it is always smaller.

Provide suitable fallbacks and inspect the page while the preferred font is
unavailable. Match metrics where practical and supported, using measured values
rather than guessed overrides. Choose a loading strategy that keeps content usable
and limits disruptive shifts. Ensure requested weights and italics exist; do not
depend on synthetic styles when they undermine the intended result.

Inspect the actual headings, controls, and initial view after font loading, not
only the token declarations. A fallback that changes wrapping can also change
action placement or clip a control.

## Define semantic color pairs

Start with roles: page and raised surfaces, primary and secondary text, rules,
interactive elements, focus, selection, and relevant status colors. Reuse the
product's semantic tokens. Keep the foreground with its background when evaluating
a pairing; a color does not have adequate contrast in isolation.

Distinguish an action signal from a broad brand field. A saturated section can
establish identity while buttons, text, and focus use separately tested roles
within it. If the same accent paints every heading, surface, link, and chart,
decide which relationships actually need emphasis and quiet the rest.

Choose a color representation supported by the project and delivery environment.
Perceptual spaces can help build related ramps, but numerical spacing does not
prove readable contrast or even visual steps in the final rendering. Inspect
actual text, icons, field edges, and focus indicators against their backgrounds.
Use the applicable accessibility standard and project requirements for compliance
claims; an alternative perceptual metric does not replace a required check.

Keep success, warning, and error meanings consistent where they apply. Pair color
with wording, shape, position, or another appropriate cue. A muted disabled
treatment still needs a discoverable explanation when the reason affects what
the user can do next.

## Derive required color schemes by role

When the product requires multiple schemes, treat each as a complete rendering
of the same hierarchy. Reassign surface, text, accent, focus, rule, and status
roles for the scheme instead of inverting the page or swapping a few hex values.
Keep established semantic meanings while adjusting pairings to remain distinct
and readable.

Inspect nested surfaces, overlays, selected controls, form errors, charts, and
imagery in each scheme. A shadow that establishes elevation on a light surface
may need a different treatment on a dark one. Choose surface steps or outlines
from the intended hierarchy; do not assume the same numerical lightness change
will work for every palette. Preserve photographs and product captures unless
an intentional, authorized treatment is appropriate.

Respect the existing preference mechanism. Where a new mechanism is in scope,
define the relationship between system preference, explicit selection, and
persistence; inspect the initial render as well as the toggle. Do not add a second
scheme merely to complete this reference.

## Worked example: a colored offer and a data table

Example brief: a product has an established blue identity, a wide blue offer
section, a plan comparison, and required light and dark schemes.

Keep the blue field as a surface role. Test its heading, explanatory text, action,
and focus separately; a darker blue button can disappear on the field even if
the same button works on the ordinary page surface. Use a suitable foreground
and action treatment on that field rather than borrowing the page's muted text
or assuming the brand accent is always the button color.

In the comparison, use the shared heading and label roles, align comparable
figures, and keep units visible. Give the selected plan a meaningful cue without
making every cell an accent. Inspect a long plan name, a larger localized price,
and fallback-font rendering before fixing column widths.

For the dark scheme, remap the table surface, row emphasis, rules, values, selected
state, and focus together. Recheck the offer's pairings in that scheme. Preserve
the information hierarchy while changing the values needed to express it.

## Verification

- [ ] Type was judged on representative real content, including relevant wrapping and languages.
- [ ] Role differences remain clear without unnecessary families, sizes, or colors.
- [ ] Font rights, loading, coverage, and fallbacks fit the delivery environment.
- [ ] Actual foreground/background pairs and meaningful non-color cues were checked.
- [ ] Every required scheme preserves readable hierarchy and relevant control states.
- [ ] Unavailable rendering or accessibility checks remain explicit limitations.
