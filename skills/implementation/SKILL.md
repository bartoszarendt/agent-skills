---
name: implementation
description: Deliver authorized changes in coherent increments with proportionate verification. Use while implementing a multi-step change or one with material implementation risk, or when executing an existing plan.
---

# Implementation

Complete the requested outcome in increments that make failures attributable
and progress reviewable. A small task may need only one increment.

## Understand the work

Inspect the relevant implementation, callers, tests, configuration, and
documentation. Check the working tree before editing and preserve unrelated
changes. Use existing mechanisms when they meet the need.

Identify the intended outcome, constraints, acceptance criteria, and any explicit
gates. If working from a plan, preserve its contracts, exclusions, and required
proof. Resolve consequential ambiguity before dependent work; continue useful
independent work that is already authorized.

For multi-step work without an existing plan, outline the increments in order
with each one's check before editing. A few lines are usually enough; state
them and continue within existing authorization, preserving explicit review
gates.

When work spans several turns, begin each progress update with the current
increment, what has changed, what verification has established or remains
pending, and the next step or blocker. When a task or plan tracker is in use,
keep it current and do not restate the full plan in prose; it does not replace
the update.

## Choose a coherent increment

Prefer one observable behavior or resolved risk. Include the layers and
necessary restructuring that make it complete. Split independent concerns when
that improves review, attribution, or reversibility.

Investigate consequential unknowns before building on them. Use a small
experiment when it can resolve the uncertainty cheaply. Keep experiments
separate from delivered behavior and account for their cleanup.

Do not split by arbitrary file counts or line limits. Do not add flags,
compatibility layers, or staged migrations unless a real rollout or consumer
commitment requires them. When such mechanisms are needed, define ownership,
safe defaults, and removal or recovery conditions.

## Implement the smallest sufficient solution

- Check whether the requested behavior already exists before adding another path.
- Prefer direct code and existing libraries or platform capabilities when they
  meet the contract clearly.
- Compare dependencies by capability and total maintenance cost. Do not recreate
  mature functionality merely to avoid adding a dependency.
- Introduce an abstraction only when it removes a demonstrated burden or
  represents a real boundary. Implementation count alone does not decide.
- Prefer clear behavior over a shorter diff. Preserve error handling, validation,
  lifecycle ownership, and accessibility that the outcome requires.

Fix defects introduced by the change. Address existing defects that block a
correct solution with the smallest necessary expansion. Report significant
independent defects without implementing unrelated cleanup.

If evidence disproves the approach, revise it. After two unsuccessful attempts
based on the same hypothesis, pause edits and reassess before another attempt.
Do not turn repeated uncertainty into more special cases.

## Verify affected behavior

Choose the narrowest check that establishes the claim: existing focused tests,
static checks, a build, a request, or a runtime scenario. Inspect coverage before
adding tests. Add or extend one only for a consequential failure existing checks
would miss; low-risk changes may need no new automated test.

Broaden verification when scope, risk, failures, or project requirements justify
it. Run checks again when subsequent edits could invalidate their results.
A clean result does not need repetition after an unrelated change.

Read the output and confirm that the intended cases actually executed. Distinguish
change-related failures, pre-existing defects, and environment failures.
Do not weaken valid assertions, suppress errors, or bypass required hooks to
obtain a passing result.

When a regression test warrants sensitivity verification, use the known-bad
version or a bounded scratch copy where practical. Preserve user work and restore
temporary state even if the check fails. Report when sensitivity is unproven.

## Continue within authorization

Make routine implementation choices independently. Ask before materially changing
the outcome, public contracts, persisted-data semantics, security boundaries,
significant cost, or irreversible behavior unless already authorized.

A plan, task, or this process does not independently authorize commits, pushes,
deployment, external communication, or shared-environment mutations. Preserve
authorization already provided; do not request it again for the same action.

Keep uncommitted changes reviewable when commits were not requested. Commit
coherent increments only when the requested workflow authorizes it.

## Report the actual result

Compare the delivered behavior with acceptance criteria as well as check results.
Do not claim completion while introduced defects or required verification remain
unresolved. Complete independent authorized work when another part is blocked.

Lead with what the request needs: the outcome, the answer, or a decision
required from the user. Then state what changed, why, what was checked, and
material gaps. A focused test run supports a focused claim. Distinguish
implemented, verified, and deployed work. Report a failure by its observed
facts first. When evidence supports a possible cause, label it as a hypothesis
and state its basis; otherwise say the cause is unknown. Record material
deviations in the existing source of truth rather than creating a parallel
report by default.

Name a next action for the user only when the user owns it, specific enough to
act on without reconstructing context. Report significant independent issues
after the main result, as separate items, unless an urgent risk such as a
security or data-integrity problem should lead. Group long lists by relation,
most consequential first, without dropping items the reader needs. Use literal,
specific wording; omit preamble, restated plans, and closing offers.

Stop temporary processes you started unless needed for the handoff. Preserve
pre-existing user processes and identify anything intentionally left running.

## Verification

- [ ] The requested outcome and applicable constraints are satisfied or gaps named.
- [ ] Increments are coherent and, for multi-step work, outlined with their checks; unrelated user work is preserved.
- [ ] Necessary fixes are complete without unrelated scope expansion.
- [ ] Relevant checks exercised the final affected behavior.
- [ ] Failures, skips, and unavailable evidence are reported accurately.
- [ ] The report leads with the outcome, answer, or required decision and includes relevant progress, failures, and remaining work without requiring the reader to reconstruct context.
- [ ] Documentation and operational consequences are accounted for where relevant.
- [ ] Commits and external actions stay within existing authorization.
