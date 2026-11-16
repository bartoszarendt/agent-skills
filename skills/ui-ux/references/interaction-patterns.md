# Interaction patterns

Use the sections relevant to the user task. Treat patterns as choices with
consequences, not mandatory components for every screen.

## Navigation and orientation

Group destinations by the user's task and the product's existing hierarchy.
Distinguish destinations from actions that change data. Keep the current location
and a usable return path apparent.

Preserve filters, selection, scroll position, and drafts on return when the task
depends on them. Account for direct entry, refresh, or deep links where supported.
Do not silently reset to the home screen because a sub-flow ends.

Choose tabs, side navigation, breadcrumbs, or an overflow menu according to the
hierarchy and space. Do not select them solely from a universal item count or
viewport threshold. Keep critical actions discoverable on smaller screens.

Use a modal for a bounded interruption when users need to stay in context.
Use a navigable screen for substantial work that benefits from history, linking,
or a stable location. Make dismissal and unsaved-work behavior explicit.

## Forms and validation

Ask only for information needed at the current point. Group related fields and
explain unfamiliar formats or consequential choices before submission.

Use persistent labels and meaningful input types. Preserve password-manager,
autofill, paste, and supported keyboard behavior. Reuse information already
supplied when the process and privacy constraints permit it.

Choose validation timing by the field and error cost. Avoid interrupting users
with errors while an incomplete value is still being entered. Validate submitted
data at the real application boundary as well as offering helpful client feedback.

Retain valid input after failure. Associate errors with affected fields and make
the recovery action clear. For several errors, an actionable summary can aid
navigation; manage focus or announcements coherently rather than announcing each
message several times.

Distinguish read-only information from an unavailable action. Explain a disabled
action's prerequisite when it helps the user proceed. Hiding a control is not a
substitute for authorization, and showing one must not leak restricted data.

Autosave changes persistence and expectations. Reuse it when already supported;
do not add draft storage merely to improve a form without considering scope,
privacy, recovery, and conflicts.

## Control states

Define the states a control actually has, not a universal list. These describe
the control itself; the outcome of an operation it starts is covered under
asynchronous operations below.

| State | Applies when | What it conveys |
|---|---|---|
| Default | Every interactive control | Its purpose and that it can be used |
| Hover | Pointer input is supported | Optional reinforcement; never the only cue to an action or information |
| Focus | Keyboard or other non-pointer navigation reaches it | A visible indicator distinct from hover and selection |
| Pressed | Activation benefits from immediate acknowledgement | That input was received, without implying the operation succeeded |
| Unavailable | The action exists but cannot be used now | That it is unavailable and, when it helps the user proceed, why |
| Selected, checked, or expanded | The control holds a choice or disclosure state | The current value, exposed to assistive technology as well as visually |

Combine states coherently: a selected item can also have focus, and an unavailable
control does not show hover feedback that suggests it will respond. Keep the
control's size and label stable across its states.

## Asynchronous operations

Represent actual state, not just animation:

| State | What the interface needs to convey |
|---|---|
| Ready | What the action will do and any prerequisite |
| Pending | That work was accepted, what remains possible, and useful progress if known |
| Succeeded | The actual result and the next available action |
| Known failure | What failed, preserved input, and a safe recovery path |
| Unknown outcome | That completion is unconfirmed and which recovery is actually available |

Prevent harmful repeated submissions while preserving useful cancellation or
navigation. A disabled button alone does not establish backend deduplication.
Do not fabricate progress percentages or show success before the contract permits it.

Offer optimistic updates only when reversal and reconciliation are supported
and the user can understand a rejected change. Restore the correct state after
failure rather than leaving the interface and stored data inconsistent.

If no status lookup or reconciliation path exists, report that gap. Do not invent
a recovery control or imply that support can resolve an outcome without evidence.

Match loading feedback to the expected wait and task. A skeleton, progress
indicator, or retained stale view can each be appropriate. Distinguish stale
content from current results when that affects a decision.

Keep the action's identity apparent while it is pending. Reserve enough room for
changing labels or progress and let explanatory text grow without displacing
nearby targets unexpectedly. Apply states only where they make sense; static
text does not need a loading, selected, or disabled variant.

For example, after a reservation request times out, retain the entered details
and distinguish unconfirmed booking from rejection. Use an existing status lookup
or safe reconciliation path before offering a retry that could reserve twice.
A spinner ending or a confirmation screen appearing does not establish success.

## Feedback and recovery

Use inline feedback where the action or data needs attention. Use transient
messages for information that can safely disappear; keep consequential errors
and recovery actions available. Do not prescribe one timeout for all messages.

Show feedback near the affected object when that gives it context. A copied
value can acknowledge completion beside its control after the clipboard operation
succeeds; an unsuccessful copy needs an available recovery rather than the same
success mark. A changed row may already make its new state clear. Avoid adding
a toast for the same result unless it adds necessary information, and preserve
an appropriate announcement for people who cannot see the change. A result users
need to retain, such as a booking reference, belongs in persistent content.

For destructive or costly actions, identify the affected object and consequence.
Use confirmation when accidental execution is consequential, or undo when the
operation is actually reversible. Do not promise undo for an irreversible effect.

Word messages for the decision in front of the user. Label a confirmation's
buttons with the action and its alternative, such as "Delete 3 files" and "Keep
files", rather than a generic acknowledgement. An error states what happened,
what the user can do next, and, where it is in doubt, whether their input was
kept. An empty state says what would appear there, and offers a way to add or
find it only when one exists and the user can take it.

For interrupted sessions, canceled work, or offline states, explain what was
saved, submitted, or lost according to actual behavior. Offline messaging does
not imply authorization to build synchronization or an offline data store.

## Motion and gestures

Give feedback without delaying the next valid action. Keep animations
interruptible and make final state correct even if motion is skipped or replaced.
Do not depend on an animation-end event to commit business state.

Respect platform gestures and avoid competing scroll, swipe, and drag regions.
Provide an alternative when a critical action requires precision or a gesture
that some users cannot perform.

## Scenario checks

Exercise the relevant transitions: invalid submission, repeated action, delayed
response, timeout after a possible write, back navigation, cancellation, and
returning to unfinished work. Choose cases from the actual risk and reuse
existing checks. Report unavailable runtime evidence explicitly.
