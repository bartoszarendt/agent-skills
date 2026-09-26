# Accessibility and adaptation

Choose checks from the platform, audience, applicable requirements, and changed
behavior. Consult current authoritative standards for exact criteria and
exceptions; these prompts do not establish compliance by themselves.

## Semantics and names

Prefer native or established accessible controls. Custom appearance does not
remove the need for role, name, value, and state.

Choose icon semantics from its use. Hide a decorative icon that duplicates
adjacent text from the accessibility tree. Give meaningful standalone imagery
an appropriate text alternative. Give icon actions an accessible name and
expose relevant selected, pressed, or expanded state.

Use structural headings, group related controls, and maintain a useful reading
order. Present status meaning in text or another accessible cue as well as color.
Do not add redundant names or announcements that make navigation harder.

## Keyboard and focus

Check that relevant actions are reachable and operable without a pointer.
Follow the expected keyboard model for the control rather than making every
visual fragment an extra tab stop.

Keep focus visible and unobscured by sticky bars, overlays, or notifications.
For a modal, manage entry, containment, dismissal, and return according to the
chosen pattern. Do not trap focus in ordinary page content.

After navigation, deletion, or validation failure, place focus where it supports
continuation. An asynchronous status update usually needs an announcement rather
than an unexpected focus move.

Provide alternatives to dragging, hover, or precision interaction where needed.
Preserve relevant browser, operating-system, and assistive-technology shortcuts.

## Forms and announcements

Keep labels available after input and connect help and errors to the relevant
controls. Do not use placeholder text as the sole instruction.

Announce consequential state changes with sufficient context, such as which
count changed or whether a submission completed. Use an appropriate announcement
mechanism without duplicating output or repeatedly interrupting users.

Allow supported autofill, password managers, and paste. Assess authentication
steps for cognitive and input barriers under the requirements that apply.

## Text, layout, and input targets

Check enlarged text, zoom, long translations, user-generated strings, and
representative narrow or wide windows. Keep essential text and actions available.

Allow labels and collections to wrap where practical. If truncation is necessary,
provide an operable way to obtain the full value for keyboard, pointer, and touch
users as applicable. A hover-only tooltip does not serve all of them.

Avoid accidental page overflow. Intentional horizontal scrolling can be appropriate
for a table or other intrinsically wide content when users can discover and
operate it. Do not collapse data into unreadable cells just to avoid scrolling.

Use the correct target-size and spacing guidance for the actual platform.
Distinguish visible icon size from its hit area and keep hit areas from overlapping.
Do not apply one numeric threshold across web, iOS, and Android units.

On relevant devices, account for safe areas, system bars, on-screen keyboards,
orientation, and resizable windows. Fixed controls must not obscure content or
the focused field.

## Contrast and preferences

Measure the actual foreground/background pair and control state. Transparency,
imagery, gradients, and overlays can change the effective contrast.

Verify required themes separately, including text, icons, controls, and focus.
Do not introduce another theme solely to complete this assessment.

Respect reduced motion and other supported preferences. Preserve understanding
when movement is removed. Provide appropriate control over distracting moving
content and avoid blocking input for presentation effects.

## Verification limits

Use automated checks for the criteria they can evaluate, and manual or runtime
checks for keyboard order, focus, announcements, and task completion. A screenshot
cannot establish screen-reader usability.

If assistive technology or the target device is unavailable, document the
unverified behavior and the checks that did run. Do not equate a checklist,
tool score, or visual inspection with a complete accessibility audit.
