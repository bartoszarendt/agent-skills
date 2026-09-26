# Test quality

Use these criteria for the risk being checked. They do not require a case for
every input, branch, or testing technique.

## Negative and boundary cases

Choose representative equivalence classes that can affect the contract:
missing or empty values, meaningful limits, malformed data, duplicates, stale
events, out-of-order operations, and terminal states.

For rejection paths whose side effects matter, assert the preserved invariant:
no partial write, no unauthorized data, safe retry, or resource cleanup.
A status code alone may not establish that protection.

For persisted or exchanged data, consider compatibility, defaults, nullability,
partial reads, and round trips where relevant. Assert ordering only when it is
part of the behavior being protected.

## Async work and isolation

Ensure that the runner observes asynchronous completion and assertion failures.
Await or return promises as appropriate; connect callbacks, workers, and streams
to the test's completion mechanism. Confirm that the intended assertions execute.

Prefer readiness signals, controllable clocks, lifecycle events, or bounded
polling over arbitrary elapsed-time sleeps. A timing-sensitive regression may
need controlled scheduling; document why the timing is part of the scenario.

Control environmental inputs that can affect the result: timezone, locale,
clock, randomness, network, generated identifiers, or filesystem state.
Record random seeds when needed to replay a failure.

Use isolated resources and failure-safe cleanup for handles, servers,
transactions, files, listeners, and subscriptions. Do not run shared mutable
fixtures in parallel unless their isolation permits it.

## Flakes

Preserve the original failure and establish a rate with bounded repetition.
Use isolation, ordering changes, concurrency, or load only when the comparison
distinguishes plausible causes.

Passing alone but failing in a suite suggests interaction or timing differences;
investigate before assigning the cause to shared state.

Retries can temporarily contain a known issue under project policy. They do not
establish that the underlying behavior is correct. Report the original failure
and the lost confidence.

## UI selectors and copy

Prefer roles, labels, and accessible names when they identify the behavior
reliably. Use test IDs when identity is the contract or no suitable semantic
selector exists. Avoid incidental DOM and CSS structure.

Assert exact copy when wording is contractual or its change would be consequential.
Otherwise protect meaning and interaction without freezing harmless wording.

Choose relevant states: loading, disabled, error, empty, focus transitions, and
accessibility semantics. Do not add every state to every test layer.

## Snapshots and visual checks

Snapshot bounded, stable output that a reviewer can assess. Prefer focused
assertions when they explain the failure more clearly.

Normalize nondeterministic details only when they are outside the contract.
Review updates against intended behavior; a changed snapshot may reflect an
authorized change or incidental structure, and should not be accepted blindly.

For visual checks, control viewport, fonts, animation, data, and relevant platform
variation. Use interaction or semantic checks when the claim goes beyond appearance.

## Property, fuzz, and performance checks

Use property tests for a meaningful invariant across a broad input space.
Keep generators valid, runtime bounded, failures reducible, and seeds replayable.

Use fuzzing where malformed or adversarial input creates a consequential risk.
Choose safety and behavior assertions according to the failure being sought;
absence of a crash may be one useful claim, but does not prove all correctness.

Measure performance with a representative workload, controlled conditions,
sampling method, and actionable baseline or budget. Separate microbenchmarks
from capacity claims and account for variation.

Do not introduce these techniques without protection that justifies their
infrastructure and maintenance cost.

## Discovery, skips, and diagnostics

Confirm the intended environment, services, runner discovery, and assertions.
A required check missing its configuration must fail or visibly report that it
did not run; it must not silently become a passing no-op.

Explain skips and quarantine according to project policy, including affected
protection and how it can be restored. Optional unsupported-platform cases do not
automatically require the same tracking process as a disabled release gate.

Keep expected and actual values and the minimum useful reproduction context.
Preserve relevant seeds, correlation IDs, versions, and timing without credentials,
personal data, or excessive dumps.

## Assess existing tests

Treat these as defects when demonstrated:

- a claimed regression test passes against the relevant known-bad behavior;
- assertions never execute or asynchronous failures escape;
- the required runner does not discover the case;
- state leakage changes results or cleanup corrupts later work;
- a required gate silently skips;
- the test claims a contract it does not observe.

Investigate sleeps, broad retries, large snapshots, heavy mocking, and duplicated
setup as signals. None is a defect solely by its presence.

Use coverage and mutation results to investigate consequential missing protection.
Do not legislate percentages, assertion counts, or a fixed distribution of test
types. Preserve useful tests while correcting incidental or defective assertions.
