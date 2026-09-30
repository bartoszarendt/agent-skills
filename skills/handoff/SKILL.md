---
name: handoff
description: Preserve the context, current state, decisions, evidence, responsibilities, and next actions needed to continue or transfer any kind of work, and resume from such a record. Use when handing work to another person, agent, team, session, or environment, when preparing a continuation record, or when picking up work from one.
---

# Handoff

Write a record that lets the recipient continue without reconstructing the
history or repeating settled decisions. The work may be software, research,
review, planning, design, writing, operations, or a mix.

## Identify the recipient

Determine who continues the work: a later session, another agent, a person, a
team, or a process on another host. Match detail and format to what that
recipient needs. An agent session needs exact paths, commands, and state. A
person needs the reasoning, decisions, and open questions more than tool detail.

When the recipient is unknown, write for a capable reader without access to
this conversation.

## Choose the destination

Use the destination requested by the user or established by the project. When
a plan, issue, pull request, or document already tracks the work, record the
handoff there or point to it rather than creating a parallel record.

Otherwise choose by recipient:

- A later session or agent on the same machine: a descriptive file in the
  operating system's temporary directory, with its full path. Use a durable
  location instead when continuation may be delayed long enough for temporary
  files to be cleaned.
- A person, or a session on another host: self-contained content in the
  conversation, or a file at a location the recipient can actually reach.

A local path is not evidence that another host or person can access it. Writing
to a shared location, posting a message, or uploading requires authorization. A
request to post the handoff to a named place authorizes that post; a general
handoff request does not authorize editing shared trackers or sending messages.
Without that authorization, prepare the content and tell the user where it
should go.

## Check the current state

Verify facts that are cheap and material before recording them. Relevant state
depends on the work:

- **Code:** working directory, branch, revision, dirty files, active operations
  such as a rebase or migration, and build or test status.
- **Investigation or research:** questions answered, hypotheses confirmed or
  ruled out and why, open leads, and sources consulted.
- **Review or audit:** what was covered, what remains, and findings with their
  status.
- **Planning, design, or writing:** accepted decisions, open options, current
  draft location, and pending feedback.
- **Operations:** changes applied to live systems, current system state,
  monitoring in progress, and the rollback path.

Record checks already run, their results, and the state they covered. Re-run a
check only when later changes could invalidate it or a required gate needs
current proof. Label unverified recollections and stale results explicitly.

## Preserve what matters

Start with when the record was written, by whom or what, and the revision or
snapshot it describes, so the recipient can judge staleness. Then use the
following sections when they carry useful information:

- **Goal and scope:** requested outcome, constraints, and deliberate exclusions.
- **Current state:** what is done, what is verified, and what is accepted by its
  owner, kept distinct. Include unfinished work and known defects.
- **Decisions:** accepted choices and their reasons, kept separate from options
  still under consideration. Include rejected approaches worth remembering.
- **Authorization:** actions already authorized, their limits, and remaining
  approval or environment gates.
- **Evidence:** checks, sources, results, dates or revisions, and limitations.
- **Next actions:** ordered concrete steps, each blocker or decision with its
  owner.
- **Pointers:** locations of documents, artifacts, repositories, services, and
  processes relevant to continuation.

Keep one next-action list. Its first item may be obtaining a decision or access;
do not invent executable work to hide a real blocker.

Point to stable documents and artifacts instead of copying them. Include in full
any findings, drafts, or reasoning that exist only in this conversation; the
recipient cannot recover them otherwise.

## Protect state and access

Do not include credentials, tokens, private keys, session data, or unnecessary
personal data. Describe the approved access mechanism without its secret value.

When the work started background processes, identify them and whether they
should remain. Stop temporary processes no longer needed; preserve pre-existing user
processes.

Writing a handoff does not authorize commits, uploads, external messages, or
deployment. Report what is local, shared, pushed, or deployed without treating
those states as interchangeable.

## Resume from a handoff

Read the record, then compare its material claims with the current state before
acting: files, branches, documents, systems, and open processes may have
changed. Resolve discrepancies from current evidence and note them.

Treat recorded authorization as the upper limit; do not infer approval the
record does not state. Authorization given for a recorded state does not carry
over when that state has materially changed. Confirm it with the user before
acting, especially when the change includes other people's work.

Re-run checks whose baseline is missing or may have moved when the next step
depends on them. Continue with the next action once the state is confirmed.
Update or retire the record when it no longer describes the work.

## Verification

- [ ] The recipient can reach the record, and the user has its location or content.
- [ ] Detail and format suit the recipient.
- [ ] Current facts, historical evidence, and unverified claims are distinguishable.
- [ ] Decisions are distinct from proposals; done, verified, and accepted work are distinct.
- [ ] Content that exists only in this conversation is included, not just referenced.
- [ ] Existing authorization and unresolved gates are preserved without expansion.
- [ ] Next actions are concrete, with owners for blockers and decisions.
- [ ] State relevant to the kind of work is captured; no secrets are included.
- [ ] When resuming, recorded state and authorization were checked against current reality.
