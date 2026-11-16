# Visual review and refinement

Use this for a visual critique, a substantial refinement, or comparison with a
brief, comp, or existing interface. Choose the relevant checks; a small adjustment
does not require a full-page review. A review request authorizes findings, not
implementation or a new visual identity.

## Establish the result being judged

Identify the intended user task, requested scope, supported surfaces, and supplied
direction. For existing products, inspect the identity, tokens, and components
the work is meant to preserve. Honor an authorized preference even when another
treatment would be your default. Familiar fonts, cards, gradients, or centered
headings are not defects by themselves.

Use representative content and states. Record enough context to make a comparison
meaningful: route or component, viewport, required theme, and relevant data or
interaction state. Reuse existing captures when they show that context reliably.

## Validate the visual evidence

Before judging a capture, confirm that it faithfully represents the requested
route and state:

- it shows the requested page or component; an unexpected login, redirect, or
  unrelated error is a wrong target unless that behavior is what is under review;
- its content, assets, and fonts appear as the product actually delivers them;
- it shows the relevant state, with intended transitions settled for a static view;
- its viewport and crop include what the finding depends on;
- sensitive or personal content is absent or appropriately protected.

Separate a capture problem from a product failure. A wrong target, an interrupted
load, or an artifact of the capture tool is a reason to recapture or resolve a
local issue when supported and within scope. A font that consistently fails to
load, a view that never leaves its loading state, or an authentication redirect
that recurs under the intended conditions is evidence: report it with the
conditions that reproduce it. An error or fallback state can also be the
requested subject of the review.

If visual access is unavailable or a valid capture cannot be obtained, state the
gap. Source inspection can support observations about implementation, but it
cannot establish the appearance of an interface you have not seen. Do not infer
the intended appearance from a capture that does not show it or invent visual
findings.

## Inspect the composition before the explanation

Look at the rendered artifact before relying on its author's rationale. Identify
what attracts attention, where reading begins, and how someone reaches the main
content or action. Then compare those observations with the task and brief.

Assess the relevant relationships:

| Area | Questions to answer |
|---|---|
| Hierarchy | Does emphasis follow the information or action people need? Are competing focal points justified? |
| Grouping | Do proximity, alignment, and boundaries communicate actual relationships? |
| Typography | Do the actual words fit their role, measure, weight, and spacing? Are secondary values still readable? |
| Color and surfaces | Do contrast, action, status, and selection retain clear meanings in required states and themes? |
| Assets | Does imagery explain or establish the intended identity? Do crop, resolution, and visual weight support the content? |
| Rhythm and density | Does spacing make related content apparent without hiding useful information? Does repetition aid scanning? |
| Range | Does the direction still work in lower sections, forms, tables, and empty or error states? |
| Adaptation | Does the arrangement remain understandable with long content, narrower space, zoom, and supported input methods? |

On a work surface, task scanning and precise information may matter more than a
large opening statement. On an expressive page, a strong visual idea may be part
of the brief. Do not apply one surface's density or rhythm rules to the other.

## Compare with a supplied reference

Compare relationships as well as individual colors or components:

- **Mass:** the relative size and weight of type, imagery, controls, and empty space.
- **Interval:** distances within groups and between larger regions.
- **Entry point:** what first attracts attention and where the eye or task goes next.

Use matching dimensions and comparable content where possible. Identify the
largest consequential divergence, then decide whether it is a defect or a justified
adaptation to real content, accessibility, behavior, or implementation constraints.
A reference is evidence of intent, not permission to copy its assets or remove
product functionality. A declared implementation constraint does not silently
waive a requested visual outcome; explain an unresolved gap.

## Separate appearance from operation

Keep three kinds of evidence distinct:

| Evidence | What it can establish | What remains to check |
|---|---|---|
| Source or static check | A rule, asset reference, semantic element, or handler exists | Whether the intended state renders and the code path works |
| Rendered capture | Visible hierarchy, wrapping, alignment, and appearance in that state | Keyboard behavior, submission, recovery, persistence, and other unseen states |
| Executed interaction | The exercised path produced the observed result | Other paths, devices, access methods, or environments not exercised |

Check applicable contrast requirements with the actual foreground/background and
state, rather than guessing from a screenshot. Exercise affected controls with
supported input methods when the environment permits. A source selector does not
prove visible focus; a network-call token does not prove a working submission.
An exit code or score does not prove the intended check ran: inspect skips,
missing browser capabilities, capture failures, and the state actually inspected.

For a redesign, ask what people could previously read, find, or do that became
harder. Retained markup alone is insufficient. Do not perform an external write
or install tools merely to complete a review without authorization for that action.

## Report and refine

Prioritize by consequence and visual impact. Fix a dominant hierarchy or content
problem before polishing a small radius difference. Distinguish:

- a demonstrated functional, accessibility, or rendering defect;
- a mismatch with the chosen direction or explicit brief;
- a contextual craft recommendation, including its benefit and trade-off.

For each material finding, give the observed location or state, consequence, and
smallest useful change. State what should be preserved. Do not inflate preferences
into universal rules, invent user research, or use a numerical taste score as proof.

For example, a hypothetical narrow-screen review might observe that a product's
delivery terms fall below a decorative image while the purchase action remains
above it. Recommend grouping terms with the offer when they are needed to decide;
preserve the product photograph if it helps identify the item. Check the rendered
arrangement and purchase behavior separately before claiming the issue resolved.

When implementation is authorized, make a coherent correction and reinspect the
affected states. Avoid expanding a visual correction into a rebrand or workflow
change. An independent view can help consequential or disputed work when available;
it is not a prerequisite for routine completion.

## Verification

- [ ] Findings are grounded in valid captures or clearly limited source evidence.
- [ ] The task, chosen direction, user preferences, and authorized scope govern the review.
- [ ] Largest consequential issues and qualities to preserve are identified.
- [ ] Comparisons use meaningful conditions; adaptations and unresolved gaps are explicit.
- [ ] Static, rendered, and interaction evidence are distinct, including checks that did not run.
- [ ] Refinement and external actions stay within authorization; improvement is not claimed from an unobserved result.
