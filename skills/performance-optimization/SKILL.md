---
name: performance-optimization
description: Diagnose and improve performance across application code, services, frontends, data processing, builds, and test suites while preserving correctness. Use for slow execution, latency, throughput, memory or resource use, startup, load time, bundle size, or regressions, including problems not yet measured, and when evaluating an optimization with material cost or complexity.
---

# Performance Optimization

Use evidence to identify the limiting work, evaluate an improvement, and decide
whether its benefit justifies the maintenance and operational cost.

## Define the problem

Identify the affected user or operation, workload, and performance requirement.
Inspect existing telemetry, benchmarks, code, and recent changes.

State a target when one exists: metric, statistic, threshold, and conditions.
If the target is unclear, establish a baseline and propose a meaningful objective.
Do not block useful diagnosis on an arbitrary number or silently turn a proposal
into a contractual service level.

A report or investigation does not authorize implementation. Load tests,
production instrumentation, paid services, and shared data changes require
authorization covering their effects.

## Measure the relevant workload

Choose the cheapest instrument that reaches the symptom: a query plan, profiler,
heap snapshot, bundle report, timing harness, or representative runtime scenario.

Control data volume, concurrency, hardware, build mode, network, and cache state
where practical. Measure cold and warm behavior separately when both matter.
Record repetitions and spread so noise is visible. Protect sensitive data in
profiles and captures.

Use production-like builds for user-facing claims. Separate controlled local
evidence from field evidence. A synthetic improvement does not establish that
deployed users received it.

## Locate the cost

Use traces, plans, measurements, and code inspection to identify where time,
allocations, waiting, or bytes accumulate. Confirm a plausible cause with a
distinguishing measurement before adding an optimization.

Consider less work, fewer round trips, better data structures, reduced payloads,
or moving non-critical work. Choose according to the measured path rather than a
fixed ordering of techniques.

For web, database, concurrency, cache, memory, computation, startup, build, or
test-suite investigation, consult the relevant sections of
[references/performance-checklist.md](references/performance-checklist.md).

## Evaluate a coherent change

Keep experiments attributable. Measure individual changes where meaningful; when
several changes are inseparable, record the combined hypothesis and limits on
attribution.

Preserve validation, permissions, ordering, durability, and required work.
If a performance trade-off changes the contract, state it and obtain
authorization before making it. Before removing, merging, or narrowing tests or
checks, identify the protection affected. Proceed when consequential failures
remain covered and required gates are preserved. If protection would be reduced,
explain the trade-off and obtain authorization unless already granted.

Treat caching as a correctness decision. Identify key inputs, scope, invalidation,
acceptable staleness, size bounds, and concurrency. Do not cache a value where the
resulting staleness violates its contract.

Measure index write costs, resource limits, and backpressure as well as the
improved read or request path. Moving cost elsewhere is not automatically a win.

## Compare and retain justified changes

Use comparable conditions for before and after measurements. Report the change
and run-to-run variation. A difference inside noise is inconclusive.

Retain changes with a demonstrated benefit that outweighs their costs. If the
performance hypothesis fails, remove only the experiment's edits while preserving
user work. A neutral timing result can still leave a justified memory or
maintenance improvement; evaluate that benefit explicitly instead of relabeling
it as a speed gain.

When a check fails, determine whether behavior regressed or the check itself is
defective. Do not weaken valid protection to keep an apparent improvement.

Record material rejected approaches in the existing task or change record when
they would otherwise be retried. Do not create a permanent ledger for every
minor experiment.

## Verify and protect the result

Run affected correctness checks and required project gates. Reuse existing
regression protection before adding a benchmark, query-count check, budget, or
monitor. Add a guard only when it protects a consequential risk at a justified
cost, and account for noise and ownership.

Stop when the agreed outcome is met, further improvement is not justified, or
the available access does not allow further checks to distinguish the remaining
causes. State what remains uncertain and what evidence would resolve it. Report
the baseline, result, conditions, correctness evidence, and limits.
Identify any deployment or field confirmation still required.

## Verification

- [ ] The affected operation, workload, and objective are explicit.
- [ ] Evidence identifies the cost, or the report states what remains uncertain
      and what evidence would resolve it.
- [ ] Any retained change is supported by evidence.
- [ ] When a change was evaluated, before and after measurements are comparable
      and include relevant variation.
- [ ] Correctness and resource trade-offs, including any reduced test or check
      protection, are understood and authorized.
- [ ] When files changed, relevant final-state checks ran without weakening
      valid protection.
- [ ] Regression protection is proportionate and reuses existing mechanisms.
- [ ] When deployed users are affected, local improvement and field impact are
      reported separately.
