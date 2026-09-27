# Performance investigation by surface

Select the relevant surface and confirm its cost with representative evidence.
The suggestions below are hypotheses and techniques, not mandatory changes.

## Web rendering and interaction

Separate initial rendering, interaction latency, navigation, and layout stability.
Use current platform metric definitions and the product's targets. Distinguish
lab conditions from real-user distributions.

Inspect:

- server response, resource discovery, and request waterfalls;
- image format, dimensions, responsive selection, and loading priority;
- font loading, fallback metrics, and layout shifts;
- JavaScript execution, third-party work, and long main-thread tasks;
- repeated rendering, layout reads and writes, and expensive effects;
- navigation caching and the security reasons behind cache policies.

Choose improvements from the trace. Do not add memoization, workers, preloads,
or virtualization without a demonstrated benefit. Do not remove a privacy or
freshness control to improve a navigation cache score.

For long operations, consider chunking, yielding, or moving suitable work off
the main thread. Verify that responsiveness improves without breaking ordering,
cancellation, or accessibility.

## Bundles and assets

Use production-like output and inspect what ships, including duplicate packages
and unexpectedly retained modules.

Consider route or feature loading, compression, caching, and unused asset removal.
Preserve modules with side effects; do not declare them side-effect-free merely
to reduce bundle size.

Set budgets from product needs and representative measurements. Reuse existing
enforcement where useful. A new CI budget needs a stable signal and ownership.

## Database access

Check query count, returned volume, round trips, execution plans, lock waits, and
connection acquisition. An N+1 pattern matters according to its workload and cost.

Compare a join, batch fetch, or revised access pattern against the required
semantics. Bound lists that can grow without limit. Choose stable pagination
ordering and handle ties when using cursors.

Inspect estimates and actual behavior where safe. Execution-analysis commands
may run the statement; check their effects before using them on shared data or
writes. Use an isolated or otherwise authorized environment.

Evaluate indexes by the query shape and measured plan, including write overhead
and storage cost. A sequential scan may be appropriate. A changed plan is not
required if the actual performance benefit is otherwise demonstrated.

Do not drop existing indexes without inspecting constraints, other consumers,
and authorization for the affected environment.

## Resource pools and concurrency

Measure time spent waiting separately from work performed. Identify connection
leaks, long transactions, uncanceled requests, locks, or downstream limits.

Compare aggregate capacity across instances with the backend's limits. Multiple
pools may be justified for separate services or credentials; avoid accidental
per-request pools.

Bound waiting, queues, and retries where overload can compound. A larger pool
can move contention into a downstream service rather than solve it.

## Caches

Establish acceptable staleness, authorization scope, key inputs, invalidation,
retention, size bounds, and failure behavior before changing a cache.

Consider:

- in-process state when per-instance differences are acceptable;
- shared caching when consistency or recomputation cost justifies the service;
- public edge caching only when responses and keys preserve privacy;
- request coalescing when overlapping misses repeat expensive work;
- negative caching when absence is safely distinguishable from provider failure.

Account for expiry storms and uncertain invalidation. Do not treat an origin
error as a cached "not found." Record hit rate and total cost; an added network
hop may outweigh the saved work.

## Memory and resource retention

Compare memory with workload, concurrency, and uptime. Growth alone does not
establish a leak; caches, heap reservation, and pending work can explain it.

Use supported profiling tools, representative operations, and comparable snapshots.
Follow retained objects to their owners. Inspect unbounded collections, listeners,
subscriptions, closures, detached UI nodes, buffers, and incomplete cleanup.

Verify release or bounded retention after work completes. Stream large data when
that preserves the required behavior and meaningfully reduces peak resource use.

## Computation and data processing

Separate CPU time from waiting on I/O, locks, or other services before choosing
a technique. Check how cost grows with input size; a small sample can hide
superlinear behavior that dominates at realistic volume.

Inspect:

- repeated work, redundant passes, and recomputation inside loops;
- data structures that fit the dominant lookups and updates;
- copying, conversion, parsing, and serialization of large values;
- file access patterns, per-item I/O, and buffering;
- per-item overhead that batching, vectorized operations, or native libraries
  can remove.

Profilers add overhead and can distort short or frequently called functions.
Use sampling for a whole-program view and timing harnesses or tracing for narrow
comparisons, with the runtime's supported tools.

Parallelism helps only when work divides and the runtime permits it. Account for
worker start-up, data transfer between workers, runtime limits such as an
interpreter lock, and contention on shared resources. Report elapsed time and
total resource use separately.

## Startup, builds, and test suites

Divide elapsed time into phases: dependency installation, compilation or
discovery, imports and initialization, setup, execution, teardown, and external
services. Use the tool's timing or duration reports before changing configuration.

Inspect:

- import-time or initialization work that could load on demand;
- the slowest tests or build steps and how total cost is distributed;
- expensive setup repeated where sharing preserves isolation;
- fixed sleeps, generous timeouts, and polling where a readiness signal or
  controlled clock exists;
- network, database, or container start-up whose cost exceeds what the
  protected risk requires;
- dependency, build, and test caches, including their invalidation keys and
  hit rates.

For a slow test, separate setup cost from the behavior under test. Share
fixtures or run tests in parallel only when isolation, ordering, and cleanup
permit it; confirm with repeated runs and changed ordering. Parallel runs can
reduce elapsed time while increasing total CPU, memory, or CI cost; report both.

Test count alone does not establish waste. Before removing, merging, skipping,
or narrowing tests, identify the failures they detect. Proceed when retained
cases still detect each consequential failure; if protection would be reduced,
explain the trade-off and obtain authorization unless already granted. Test
selection and result caching can speed iteration; do not let them replace
required gates without authorization.

## Evidence

Record command or instrument, build, environment, workload, cache state,
repetitions, spread, and observed result. Keep personally identifying or
secret data out of captures.

Use an existing performance guard when it covers the risk. Add a new guard only
when its protection outweighs runtime, noise, and maintenance costs.
