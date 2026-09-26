# Decision record format

Use the repository's existing decision-log location, numbering, markup, and
lifecycle. Do not create a second convention.

## Minimal record

A short paragraph is sufficient when it preserves the reason:

```markdown
# Use SQL for the reporting queries

The reporting queries require database features that the current abstraction
does not expose adequately. Keep those queries as parameterized SQL with the
existing integration checks; retain the abstraction for ordinary application
access. This limits custom SQL to the area with a demonstrated need.
```

Record evidence behind consequential claims. Do not invent benchmark numbers
or alternatives merely to complete a template.

## Expanded record

Add sections only when they carry useful information:

```markdown
# <decision>

Status: proposed | accepted | superseded
Date: <date>

## Context
<requirements, constraints, and verified facts>

## Decision
<chosen or proposed behavior, with its authority clear>

## Rationale
<why it fits the current needs>

## Alternatives
<rejected options worth remembering and the reason>

## Consequences
<non-obvious costs, migration needs, or operational obligations>
```

If there is no established location and a separate record is justified, use
`docs/adr/NNNN-slug.md`. Take the next available number according to the
repository's sequence. Do not renumber existing records or fill historical gaps
merely for appearance.

## Lifecycle

Preserve the reasoning of an accepted historical decision. Correct factual errors
with a clear dated amendment where needed; do not silently rewrite history as if
a later choice had always applied.

For a materially changed decision, create a superseding record when the project's
convention calls for one and link both directions. If only part is superseded,
identify that part.

A proposed record does not authorize implementation. Keep acceptance and the
relevant owner or project gate explicit when approval is required.
