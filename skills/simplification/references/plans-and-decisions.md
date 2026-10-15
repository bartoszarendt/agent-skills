# Simplifying plans and decisions

Use these signals to locate a possible burden in a proposal, plan, design,
technical decision, or process around the work. Confirm a concrete cost and a
better alternative before recommending a change.

## Separate the result from the mechanism

Restate the required result in observable terms: what users or consumers can
do, and which constraints must hold. Then list each mechanism the proposal
introduces, such as a service, datastore, queue, cache, registry, abstraction
layer, configuration, migration path, flag, document, tracker, or review step.

For each mechanism, name the current requirement it serves. A mechanism with no
current requirement is a candidate for removal or deferral. A mechanism with a
requirement is a candidate for a simpler substitute that meets it fully.

Do not narrow the result because a smaller version is easier to plan or build.
When the requested result seems larger than the need, raise the narrower option
with its trade-off and let the user or responsible owner decide. Preserve expressly
required mechanisms and binding decisions unless their change is already
authorized. A mechanism mentioned as background or proposed for review is not by
itself a requirement.

## Scope and tasks

Investigate future scale without consumers, migration machinery without a
compatibility commitment, safeguards without a reachable failure, generality no
consumer has requested, and tasks or dependencies that contribute neither
required behavior nor necessary evidence.

Preserve current acceptance criteria, known consumers, measured constraints,
approved transitions, consequential gates, and protection for irreversible
effects.

## Technical decisions

Investigate:

- a new service, datastore, queue, or cache before the current one is shown to
  be insufficient;
- custom construction of what an adopted platform, framework, or dependency
  already provides;
- a new dependency or tool for what existing ones or a few lines of direct code
  cover reliably;
- an abstraction or configuration added only to postpone a choice.

Compare realistic alternatives, usually the current state, an existing
mechanism, and the proposal. Routine choices need a short rationale; reserve
structured comparison for decisions that are costly to reverse, such as
persisted data formats, public interfaces, security boundaries, and long-term
vendor or infrastructure commitments.

Keep a decision open only when information expected later would change it and
waiting costs little. Otherwise choose a supported default within existing
authorization, preferring the option that is cheaper to reverse when uncertainty
is material.

Preserve approved decisions unless their change is already authorized. Use the
project's established decision process for changes outside that authorization;
a simpler alternative does not itself authorize reopening a decision.

## Process, tracking, and documentation

Investigate status tracked in several places, documents that restate another
source of truth, reports nobody uses for a decision, approval steps no policy or
risk requires, and handoffs that add waiting without adding information.

Retain one usable source of truth, required gates, and records that later work
or audits depend on. Removing a manual step that protects an irreversible,
shared, or external effect is a change to a control, not a simplification.
Moving automated work into repeated manual steps adds burden; count it.

## Deferrals and bounded choices

Record a deferred capability as remaining scope: what is excluded, its
consequence, who authorized the deferral, and the observable condition that
would bring it back. Do not present deferred work as complete.

When later work depends on a bounded choice's limit, or a reader could mistake it
for an oversight, record the assumption, limit, and observable condition for
revisiting it where implementers will see them, such as the task contract,
decision record, or plan's boundaries.

## Proposing reductions

For each proposed reduction, state what is removed or replaced, the requirement
it served or the absence of one, what still guarantees the outcome, and the
remaining cost. Describe the reduction by the elements removed, such as tasks,
services, dependencies, steps, or documents, rather than by unsupported effort
or percentage estimates.

A request to review a plan or decision does not authorize editing it. When
edits are authorized, preserve the plan's identifiers, approved decisions, and
acceptance mapping, and record material scope changes with their authorization.
