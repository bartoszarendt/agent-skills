---
name: task-handoff
description: Preserve the verified state, decisions, authorization, and next actions needed to continue work in another session or environment. Use when the user requests a handoff or work needs an explicit continuation record.
---

# Task Handoff

Write a concise record that lets the next session continue without reconstructing
the conversation or repeating settled decisions.

## Choose the destination

Use the destination requested by the user or established by the project.
If neither exists, use a descriptive file in the operating system's temporary
directory and provide its full path.

If the next session runs on another host, distinguish local files from transferred
artifacts. A temporary path on this machine is not evidence that another session
can access it. Provide the content or an authorized transfer method when needed.

## Check the state

Verify facts that are cheap and material: working directory, branch, relevant
revision, dirty files, active operations, and artifact locations.

Record the commands already run, their results, environment, and the state they
covered. Re-run checks only when changes could invalidate the evidence or a
required gate needs current proof. Label unverified recollections and stale
results explicitly.

## Preserve what matters

Use the following sections when they carry useful information:

- **Goal and scope:** requested outcome, constraints, and deliberate exclusions.
- **Current state:** delivered behavior, unfinished work, defects, and relevant
  worktree or remote state.
- **Decisions:** choices and reasons, including rejected approaches worth remembering.
- **Authorization:** actions already authorized, their limits, and remaining
  approval or environment gates.
- **Evidence:** checks, commands, results, dates or revisions, and limitations.
- **Next actions:** ordered concrete steps, with blockers and decision owners.
- **Environment and pointers:** repository paths, branches, documents, artifacts,
  services, and processes relevant to continuation.

Keep one next-action list. Its first item may be obtaining a required decision
or environment access; do not invent executable work to hide a real blocker.

Point to stable documents and artifacts instead of copying their contents.
Include enough reasoning to explain choices that are otherwise unrecoverable.

## Protect state and access

Do not include credentials, tokens, private keys, session data, or unnecessary
personal data. Describe the approved access mechanism without its secret value.

Identify background processes started for the task and whether they should remain.
Stop temporary processes no longer needed; preserve pre-existing user processes.

Creating a continuation record does not authorize commits, uploads, external
messages, or deployment. Report what is local, shared, pushed, or deployed
without treating those states as interchangeable.

## Verification

- [ ] The record has an accessible destination and the user has its path or content.
- [ ] Current facts, historical evidence, and unverified claims are distinguishable.
- [ ] Scope, decisions, existing authorization, and unresolved gates are preserved.
- [ ] Next actions are concrete and acknowledge real blockers.
- [ ] Relevant worktree, environment, artifact, and process state is captured.
- [ ] No secrets or unnecessary personal data are included.
