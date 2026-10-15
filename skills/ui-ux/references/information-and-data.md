# Information and data presentation

Start from the decision the reader needs to make. Choose a representation that
preserves meaning at the relevant volume, precision, and interaction cost.

## Choose a representation

| User need | Useful starting point | Check before choosing |
|---|---|---|
| Find a record or exact value | List or table with relevant search or filters | Identity, precision, scan order, volume |
| Compare categories | Aligned bars or a comparison table | Shared scale, ordering, long labels |
| Understand change over time | Line chart or another time-based view | Sampling, gaps, time range, units |
| Understand a distribution | Histogram, box plot, or plotted observations | Bin choice, outliers, sample size |
| Understand proportions | Stacked bars or a small part-to-whole view | Denominator, category count, comparison difficulty |
| Inspect relationships | Scatterplot or linked detail | Overlap, scale, and whether association is being overstated |

These are starting points, not an industry-to-layout mapping. Use a table when
the task needs exact comparison rather than adding a chart for decoration.

## Preserve data meaning

Label units, time granularity, date range, and relevant timezone. Keep number
formatting and precision consistent with the domain. Distinguish zero, missing,
not applicable, loading, stale, and failed data.

Make filtering, aggregation, sampling, and omitted values apparent when they
affect interpretation. Do not silently remove outliers or imply that unavailable
data is zero. Use truthful axes and disclose changes of scale that affect comparison.

Choose direct labels, legends, annotations, or accessible descriptions according
to the reading task. Do not require a separate legend when labels already carry
the meaning. Avoid relying on color alone for series or status identification.

## Tables, filters, and actions

Keep row identity, essential columns, and action scope clear. Indicate the active
sort and filters. Distinguish selection on the current page from selection across
all results before a bulk action.

Preserve state when returning from a detail view where that supports the task.
Define what happens when selected rows disappear, permissions change, or refreshed
data no longer matches a filter.

For no results, distinguish an empty dataset from filters that exclude all rows
and offer an appropriate recovery. Do not show a creation action when the user
lacks that capability.

Add sorting, export, search, or drill-down only when the task requires it or the
benefit justifies the scope. A table is not an instruction to implement every
data-management feature.

## Charts and constrained layouts

Choose the representation from the reader's job before assigning color. Use
color for identity, magnitude, polarity, or status, and keep that role
consistent within a view. Do not choose a palette first and then fit the data
to it.

Prefer separate charts, small multiples, or a shared index over two y-axes for
comparing measures; a second scale makes slope and crossing comparisons
arbitrary. When a second axis is required, label both scales and units and
state the limits of comparing them visually.

Assign categorical hues in a stable order. When series outnumber the hues that
stay distinguishable, choose by the reader's task: group a remainder, use small
multiples, or add a non-color encoding such as direct labels, markers, or line
styles. Do not invent near-duplicate hues to keep every series separate.

Keep a series' color attached to the entity it names: changing what is shown,
such as an active filter, must not repaint the surviving series. Prefer text
colors for values and labels, with a colored mark beside them; use a series
color for text only when it meets text contrast.

For magnitude, use an ordered light-to-dark scale, either single-hue or a
perceptually ordered multi-hue scale; for polarity, use two hues around a
neutral midpoint. Avoid rainbow scales, whose hue steps suggest boundaries the
data lacks. Reserve status colors for status, including series that represent
statuses, and do not use them to identify unrelated series.

Do not rely on color alone for identity, status, or value; add another cue,
such as text, shape, an icon, or position. Do not claim that a palette remains
distinguishable without color vision, or in a required theme, unless a check
such as a simulation or computed color difference established it; visual
inspection alone is not that check.

Keep important comparisons and exact values accessible without relying only on
hover. Provide a useful summary, equivalent table, or other accessible access
to the information appropriate to the task and data size.

Interactive controls need the applicable keyboard and touch behavior. A static
chart does not require every data point to become a separate focusable control.

Adapt labels, ticks, orientation, or the representation for constrained space.
Preserve relevant detail through accessible drill-down when supported. Consider
aggregation or virtualization only when workload and readability justify it;
do not use a universal point-count threshold.

## Badges, chips, and compact content

Distinguish status, a selectable filter, and a removable value. Give actions and
state the correct semantics rather than making every badge clickable.

Let collections wrap before shrinking useful labels. An overflow summary should
reveal the hidden values when users need them; a count alone may hide the
information required for a decision.

Announce meaningful count or status changes in context without moving focus.
Do not depend on micro-animation to communicate the final value.

## Verification

Use representative long names, missing values, large and small numbers, active
filters, and relevant data volumes. Confirm the user can make the intended
comparison and reach required actions with supported input methods. For a
chart, confirm surviving series keep their colors when filters change, meaning
does not depend on color alone, any second y-axis was required and labeled,
and no color-vision claim lacks a check.

Check measured performance when volume creates a concern. Report which scenarios
were exercised; sample screenshots are not evidence that real data paths work.
