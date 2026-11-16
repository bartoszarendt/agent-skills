# Visual direction

Use this reference when creating a substantial new surface, choosing an identity,
or resolving an unclear visual direction. For a focused component correction,
use the established system and change only what the problem requires.

## Derive the direction from evidence

Identify the task, audience, available content, and context of use before choosing
an aesthetic. Consider frequency of use, decision complexity, expertise, and the
amount of information people need at once. A public introduction and a daily
operations tool can share an identity while needing different density and pace.

Look for material specific to the subject: actual products, documents, locations,
units, terminology, working methods, or supplied imagery. Distinguish verified
facts from possible creative associations. Do not invent a founder's story, a
craft tradition, or customer preferences to justify a direction.

When the user supplies references, identify what each demonstrates: hierarchy,
typography, composition, color relationships, imagery, density, or interaction.
Describe the relevant relationship and adapt it to the actual content. A screenshot
does not establish how a control works or grant permission to reuse its assets.
Resolve conflicting references through the brief and existing identity; ask only
when the remaining choice materially changes the outcome.

## Turn an idea into usable rules

Choose a central idea that helps explain or use the product. State it briefly
when doing so will guide implementation or review. A token adjustment does not
need a concept statement, a separate design document, or a presentation of options.

Translate the idea into decisions that can be applied beyond the first screen:

| Decision | Establish |
| --- | --- |
| Typography | Which content leads, how detail is distinguished, and how dense text reads |
| Composition | How related information aligns, groups, and changes at constrained widths |
| Color | Which roles identify actions, states, surfaces, and supporting information |
| Components | How controls, tables, forms, and feedback express the same hierarchy |
| Assets | What the user needs to see and how imagery or diagrams explain it |
| Motion | Which changes need continuity or feedback and which can be immediate |

Reuse sound existing decisions. Explore alternatives when the brief leaves a
meaningful choice unresolved or the first direction fails its content. Compare
their suitability and implementation cost; do not produce a fixed number of
options or select novelty for its own sake.

Use subject-specific details where they carry meaning. A real unit can label a
value; a real document structure can organize information. Decorative gauges,
stamps, or technical notation need a reason beyond making a generic layout look
special. Keep navigation, action labels, and control semantics recognizable.

## Starting values for a new system

When a new surface has no established tokens, these values can start the work.
They are adjustable defaults for readability and rhythm, not quotas or quality
gates, and existing project tokens take precedence. Accessibility requirements,
such as contrast, target size, and text resizing, apply separately under the
applicable standard and are not satisfied by these values.

| Area | Starting point | Adjust when |
|---|---|---|
| Running text | About 16 CSS px on the web, line height about 1.4 to 1.6, measure about 45 to 75 characters | The face's proportions, the script or language, or short scanned labels rather than prose call for it |
| Headings | Line height about 1.0 to 1.25, tighter as size grows; size steps around 1.2 apart for a dense tool, 1.25 to 1.5 for an expressive page | Headings often wrap, translations run longer, or the tool needs quieter hierarchy |
| Spacing | Steps from one base unit, such as 4 or 8 px, with less space within a group than between groups | Density, input method, or content volume calls for a tighter or looser rhythm |
| Motion | About 100 to 200 ms for small feedback such as a press; about 200 to 400 ms for panels and larger transitions; easing out on entry and in on exit | The distance is large, the change is frequent, or reduced motion is requested |

Check the result on actual content and change a value when the rendered text,
groups, or transitions show that it does not fit. Record the values the system
adopts in the project's existing token mechanism rather than a separate document.

## Carry the direction through the full surface

Check that the direction survives ordinary content: long headings, a form, a
comparison, an empty result, and a dense list where those occur. If the identity
only works with a large photograph or a short slogan, extend the underlying rules
before decorating more sections.

Use different expressions of the same system where the task needs them. An
expressive introduction can lead into quiet buying information; an application's
summary can use more space than its editable table. Preserve related type roles,
alignment, colors, and state conventions without forcing identical layouts.

Apply visual emphasis to the content or action that matters at that point in the
task. Repetition can help comparison; variation can mark a change in subject or
pace. Do not alternate layouts or add sections merely to avoid repetition.

## Worked example: a repair service

Example brief: a repair service supplies bench photographs, a service list, an
intake form, and a technician's repair queue. The public page must help visitors
decide whether to request a repair; technicians use the queue repeatedly.

Derive a direction from the inspection process: clear item identification,
findings, and the next useful action. Use aligned labels and values, legible
technical detail, and a strong distinction between information and commands.
Do not decorate every section with bolts or make controls resemble machinery.

On the public page, use a relevant bench photograph to establish the work, place
the service scope near the intake action, and show supplied prices or conditions
where people decide. Carry the same alignment and type hierarchy into the service
table, form labels, errors, and contact information. The lower page should remain
recognizable when the photograph is out of view.

In the technician tool, retain the established vocabulary and shared visual roles,
but prioritize scanning the queue, distinguishing actual repair states, and finding
the next action. Use compact rows and stable columns where they help. Do not add
a promotional hero, large scenic imagery, or extra spacing that displaces the work.
Changing either surface's business rules remains outside a visual design task.

## Worked example: an exhibition page

Example brief: a museum supplies installation photographs, credited images of
the prints on show, a talks schedule, ticket prices, opening hours, and access
information for a temporary printmaking exhibition. Visitors decide whether and
when to visit; most arrive once.

Here the works are the content and visits are occasional, so the direction can
be slower and more expressive than the repair queue. Derive it from the medium:
ink on paper, registration, and edition numbers. Use a paper tone for the page
surface and one ink color drawn from the actual works for links and selection,
tested as a text pair against that surface. Set the exhibition title and section
openings in an expressive display face, and essays in a quiet text face at the
running-text starting values above. Use the expressive end of the heading steps,
since there are few headings and a short title. Give each work generous space
and keep its credit grouped closely beneath it.

Show prints uncropped, at a size where their printed detail is legible; they
carry information, so they crop less freely than an atmospheric installation
view. Keep hours, prices, access information, and the ticket action in a plain,
aligned block near the opening and again at the end; expression must not obscure
them. Set the talks as an aligned list with dates, times, and speakers rather than
decorative tiles, with tabular figures for times.

Do not invent an artist's quote, lay a print texture over running text, or crop
a work to fit a grid. Where a credit, price, or time is missing, leave a marked
placeholder rather than a plausible value.

## Review the direction

Inspect representative screens in context, including later sections or working
states. Ask whether the distinctive choices come from this subject and whether
they improve comprehension, identity, or task completion. A familiar pattern can
be the best answer; a design does not fail because another product uses it.

When a rendered view is available, inspect hierarchy at a glance and then inspect
the actual words and controls. A blurred or reduced view can reveal competing
emphasis, but cannot establish readability, interaction correctness, or usability.
Compare with the requested identity and outcome rather than an unrelated ideal.

## Verification

- [ ] Consequential visual choices follow the brief, content, and context of use.
- [ ] References informed specific decisions without importing unsupported behavior or rights.
- [ ] The direction remains coherent in relevant forms, data, lower sections, and states.
- [ ] Density and emphasis support the task without unnecessary novelty or scope growth.
- [ ] Rendered observations and unverified design hypotheses are reported separately.
