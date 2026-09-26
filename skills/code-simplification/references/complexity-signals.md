# Complexity signals by surface

Use these signals to locate a possible burden. Confirm a concrete cost and a
better alternative before recommending a change. The exceptions explain why
an apparently unnecessary mechanism may still be justified.

Choose among removing work, direct use, local helpers, shared mechanisms, and
new abstractions according to the actual need. Do not apply a fixed ladder
without checking what responsibility each option preserves.

## Local structure

Investigate forwarding wrappers, re-export-only files, unclear names, repeated
conditions, speculative options, and multiple owners of the same state.

Preserve useful domain names, type narrowing, centralized policy, external
interfaces, and lifecycle ownership. A wrapper can simplify the caller even
when its implementation is small.

## Proposals and scope

Investigate future scale without consumers, migration machinery without a
compatibility commitment, and safeguards without a reachable failure.

Preserve current acceptance criteria, known consumers, measured constraints,
approved transitions, and protection for irreversible effects. Do not narrow
a user's explicit outcome merely because a smaller version is easier.

## Architecture and data flow

Investigate layers that add coordination without a responsibility, duplicate
models with no distinct role, broad registries, and shared modules accumulating
unrelated cases.

Preserve stable domain boundaries, deliberate isolation, ownership, external
contracts, and lifecycle control. One implementation does not by itself make
an adapter unnecessary.

## Tests

Investigate fixture hierarchies, elaborate case languages, repeated assertions
with no distinct protection, and helpers that obscure the oracle.

Preserve unique protection for contracts, wiring, persistence, permissions,
concurrency, compatibility, and cleanup. Shared setup can be useful when it keeps
cases clear; duplication can be useful when abstraction would obscure behavior.

Consolidate directly affected redundancy without broadening into suite cleanup.

## Configuration

Investigate settings nobody uses, impossible combinations represented as valid,
and configuration that duplicates another source of truth.

Preserve real deployment differences, operator controls, secret boundaries,
supported environments, and meaningful user choices. Check consumers before
removing an apparently unused option.

## Dependencies

Investigate overlapping packages, custom wrappers with no responsibility, and
new infrastructure introduced before existing capabilities were considered.

Compare alternatives by capability, security, maintenance, compatibility, and
operational cost. A mature library can be simpler to own than a short custom
implementation with hidden edge cases.

## Concurrency and resilience

Investigate queues, caches, retries, locks, and state machines whose costs have no
demonstrated benefit.

Preserve mechanisms needed for realistic overlap, shared mutable state,
non-idempotent effects, cancellation, cleanup, availability commitments, or
unknown external outcomes. Low user count does not eliminate concurrency risk.

## Validation and security

Investigate duplicate checks that protect the same boundary without carrying
additional information, or defensive branches for demonstrably impossible inputs.

Preserve parsing at trust boundaries, operation-level authorization, business
invariants, and constraints against alternate writers or concurrent changes.
Carry validated knowledge forward when it remains valid.

If the purpose of a control is uncertain, investigate before removing it.
Ask when the remaining uncertainty affects the security boundary; do not remove
the control to simplify the code while the question remains.

## Compatibility and fallbacks

Investigate silent fallback chains, adapters with no known consumer, and temporary
paths with no ownership or removal condition.

Preserve established support, approved migrations, and deliberate recovery
behavior. Not every fallback is temporary; document its contract when it is a
supported part of the product.

## Operations

Investigate duplicate telemetry, unused flags, and recovery mechanisms that do
not support a real operational decision.

Preserve diagnostics needed for incidents, required availability, destructive
operations, reconciliation, and rollback. A local reduction in code can increase
operator burden; include that cost in the decision.

## Suggestions that add complexity

Apply the same scrutiny to a proposed fix. Establish the defect, affected scope,
and reason for a new abstraction, check, dependency, or persistent state.

Prefer the smallest coherent correction. Implement feedback only within the
authorized task; a reviewer's suggestion is evidence to assess, not independent
permission to change the system.
