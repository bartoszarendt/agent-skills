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
comparison and reach required actions with supported input methods.

Check measured performance when volume creates a concern. Report which scenarios
were exercised; sample screenshots are not evidence that real data paths work.
