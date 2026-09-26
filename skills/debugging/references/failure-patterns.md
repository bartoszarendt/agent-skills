# Failure patterns

Use these patterns to narrow an investigation. Confirm the suspected cause;
a familiar symptom does not establish the diagnosis.

## Tests and builds

For a failure after an edit, inspect the changed behavior, test contract, fixtures,
and environment. A test outside the edited files can still be affected by shared
state or imports, but it can also reveal a pre-existing or unrelated failure.

Run the relevant case in isolation when that distinguishes the hypotheses.
Passing alone but failing in a suite suggests ordering or resource interaction;
it does not rule out timing-sensitive application defects.

For build failures, inspect:

- cited types and the values or signatures that produced them;
- module existence, exports, resolver settings, and platform path differences;
- configuration schema and supported tool versions;
- manifest, lockfile, installation state, and generated artifacts;
- differences between the local and CI environment.

Correct demonstrated test defects deliberately. Preserve unrelated valid
assertions and do not skip a check merely because it is inconvenient.

## Runtime failures

Trace the value and lifecycle that lead to the symptom. For nulls, identify the
producer and expected absence behavior. For retry-only failures, inspect stale
state, resource cleanup, partial effects, and deduplication.

For a blank UI, inspect console, network, error boundaries, and state transitions
before changing rendering. For a slow path, establish a representative
measurement before selecting an optimization.

## Intermittent or unavailable reproductions

Compare timing, runtime versions, data shape, configuration, locale, and state.
Use redacted inputs and isolated resources.

Establish an observed failure rate with bounded repetitions. Vary one meaningful
condition when practical: isolation, order, concurrency, or load. Do not run a
shared database suite in parallel unless its isolation supports that execution.

Use readiness signals, controllable clocks, or bounded polling instead of
arbitrary sleeps. Timing injection can help expose a race in a temporary harness;
it is not a production workaround.

If a rare event cannot be reproduced, preserve evidence and narrow the next
observation needed. Permanent instrumentation requires a useful signal, bounded
data, and an authorized deployment. State when the cause remains unconfirmed.

## State pollution and bisection

Record the unwanted state and establish its baseline. Isolate candidate test
groups or prior operations, shrinking the sequence that produces it. Preserve
necessary ordering: a contaminating interaction may require several tests.

For a regression between revisions, use an isolated checkout or safe bisection
workflow that preserves the user's tree. Distinguish skipped or untestable
revisions from good ones. Restore only temporary state owned by the investigation.

## Temporary containment

Contain a failure only when the behavior is acceptable under the contract or
explicitly authorized. Examples include a visible unavailable state for a
non-critical feature or a documented configuration default.

Do not use a fallback to hide invalid state, bypass a security control, or
declare an unresolved defect fixed. Record limitations, follow-up ownership,
and the condition for removing temporary containment.

## Instrumentation and cleanup

Capture the minimum data needed to distinguish hypotheses. Redact before
logging; avoid credentials, tokens, personal data, and full request bodies.
Use a marker for temporary logs and remove them after diagnosis.

Retain operational diagnostics that have an ongoing purpose. Remove owned
harnesses and processes no longer needed, and document anything left running.
