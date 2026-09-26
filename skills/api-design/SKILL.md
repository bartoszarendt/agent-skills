---
name: api-design
description: Define programming contracts for service endpoints, module APIs, functions, and component props. Use when introducing or evolving a software boundary, preserving consumer compatibility, or making an operation safe to retry.
---

# API Design

Make the contract clear enough that callers can use it correctly without
reconstructing its implementation. Keep the interface no larger than current
needs justify.

Here, an interface is a contract consumed by code. This scope includes internal
APIs and component props as well as network endpoints; it excludes screen layout,
visual styling, and user journeys.

## Inspect the existing contract

Read consumers, implementation, tests, schemas, and documentation. Identify
intentional behavior, supported consumers, and incidental details.

Define the terms used by the interface. Resolve overloaded names and conflicting
meanings with concrete scenarios. Follow existing conventions for names, error
formats, units, timezones, and serialization unless a change is justified.

A design request authorizes analysis and proposals. Implement only when requested
or already within an authorized change. Resolve material changes to public
contracts, data semantics, or security boundaries before dependent work.

## Place boundaries deliberately

Put behavior behind a boundary when it centralizes a real responsibility,
enforces a policy, isolates an external dependency, or simplifies consumers.

Prefer a small interface that hides useful complexity. Do not enlarge a module
merely to make it "deep," or delete a naming wrapper solely because it forwards
a call. One implementation can justify a real boundary; several implementations
do not automatically justify a general abstraction.

Expose dependencies when that clarifies ownership and permits useful
verification. Avoid configuration options, factories, or extension points for
hypothetical consumers.

## Specify observable behavior

State what types alone cannot express:

- valid inputs, units, defaults, and ownership;
- outputs, ordering guarantees, and generated fields;
- errors callers must distinguish and how they are represented;
- side effects, concurrency, partial failure, and cancellation;
- retry behavior and any relevant resource or performance limits.

Use the repository's error strategy consistently within a surface. Distinguish
cases callers handle differently without exposing sensitive internals.
Different operations may intentionally use different absence or error semantics;
document those differences rather than forcing one representation everywhere.

Separate input from output when their fields or guarantees differ. Use distinct
identifier types or explicit state models when they prevent plausible misuse.
Do not introduce type machinery for distinctions that have no practical effect.

## Validate according to trust and invariants

Parse and validate external input at entry boundaries, including configuration,
third-party responses, and persisted data whose provenance or version is uncertain.

Carry validated knowledge through internal contracts where it remains valid.
Avoid repeating the same check without a distinct failure path.

Enforce authorization at the operation or an equivalent boundary that covers
every caller. Preserve business invariants and database constraints where
concurrent work or alternate writers can invalidate earlier checks. Being stored
in your own database does not establish that a value meets the current contract.

## Evolve according to actual commitments

Identify consumers and compatibility expectations before changing behavior.
For established interfaces, prefer compatible additions when they solve the need.
Check additions too: strict consumers, defaults, or serialization can make an
apparently optional field consequential.

For breaking changes, define migration, upgrade, and recovery implications.
Use parallel versions only when consumer needs justify their maintenance cost.
For experimental interfaces without established commitments, prefer a coherent
design over unnecessary compatibility layers.

Do not assume every incidental behavior is a permanent contract. Investigate
documented support, actual use, and the cost of changing it.

## Design network operations for their workload

Bound lists that can grow without limit; use pagination or another explicit bound
that fits consumer needs. A fixed, small enumeration does not need pagination
solely because it is a list.

Choose update semantics deliberately. Partial updates can reduce accidental
overwrites, but do not replace version checks or other concurrency controls
when competing writes matter.

For operations that may be retried, determine whether repetition is naturally
safe or requires deduplication. For external effects, uncertain outcomes, and
idempotency keys, read [references/retry-safety.md](references/retry-safety.md).

## Verify the contract

Exercise representative consumers and consequential error or concurrency paths.
Reuse existing checks before adding new cases. For a changed public interface,
check compatibility using the relevant consumers or contract fixtures.

Update the existing documentation or schema source. State what was verified and
which consumer, provider, or runtime assumptions remain unproven.

## Verification

- [ ] The boundary has a current responsibility and a clear consumer contract.
- [ ] Names, errors, units, and state representations fit the existing surface.
- [ ] Validation, authorization, and invariants cover their actual failure paths.
- [ ] Compatibility decisions follow real commitments and authorization.
- [ ] Resource limits and retry behavior match the operation's risks.
- [ ] Relevant consumer and failure scenarios were checked, with gaps identified.
