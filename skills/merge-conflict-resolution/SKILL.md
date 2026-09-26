---
name: merge-conflict-resolution
description: Resolve Git merge, rebase, or cherry-pick conflicts by recovering each side's intent and checking the combined behavior. Use when a requested branch update or integration encounters conflicts.
---

# Merge Conflict Resolution

Preserve compatible intent from both sides and verify the combined result.
A clean textual merge does not establish correct behavior.

## Inspect the operation

Check the working tree, staged changes, active operation, base, and commits being
combined. Preserve unrelated changes and any resolutions already made by the user.

Determine whether the request authorizes only resolving files or also completing
the integration. A request to perform a merge or rebase normally covers its
continuation; merely encountering conflicts does not authorize new history changes.

## Recover intent

Read each side's relevant commits, callers, tests, and documentation. State what
each side intended before choosing a resolution.

In a merge, "ours" is the current branch and "theirs" is the incoming branch.
During a rebase, "ours" is the base plus work already replayed, while "theirs" is
the commit being replayed. Inspect the actual stages rather than relying on the
labels alone.

## Resolve coherently

Preserve both intentions where compatible. Where they conflict, use the stated
integration outcome and applicable contracts. Ask before choosing a resolution
that materially changes an unresolved requirement, public contract, persisted
data, or security boundary.

Make the glue changes necessary for the combined implementation. Do not invent
unrelated behavior or accept a whole side without inspecting what would be lost.

Resolve source inputs before regenerating lockfiles, compiled output, or other
generated artifacts with the project's tooling. Use the recorded manager and
version; inspect the result for unrelated dependency changes. Follow explicit
project handling for generated files that cannot be regenerated locally.

Search for remaining conflict markers and semantic mismatches outside the hunks:
renamed symbols, stale callers, changed defaults, and incompatible schemas.
Distinguish real markers from intentional examples or fixtures.

## Verify and continue

Run focused checks for the combined behavior and required project gates. Broaden
when the integration surface or failures justify it. Fix defects introduced by
the resolution without masking existing failures.

Stage only resolved task files. Continue the merge, rebase, or cherry-pick when
that completion is authorized, checking each later conflict against the current
state. Do not push unless the requested workflow covers it.

Abort only when authorization covers returning to the pre-operation state.
Inspect what would be discarded, including manual resolutions. If the operation
appears mistaken, explain the issue and preserve state while resolving the choice.

## Verification

- [ ] The active operation and both sides' intent were identified.
- [ ] Compatible changes and unrelated user work were preserved.
- [ ] Material trade-offs were resolved within authorization.
- [ ] Source and generated artifacts agree, with no unintended markers or stale callers.
- [ ] Relevant checks exercised the combined result, or limitations are stated.
- [ ] Continuation and any external actions stayed within the requested workflow.
