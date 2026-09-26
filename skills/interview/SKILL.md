---
name: interview
description: Clarify a proposal through focused questions, evidence, and explicit decisions. Use when the user asks for an interview or a question-led examination of an idea, design, or plan.
---

# Interview

Establish the intended outcome, constraints, and decisions that matter before
turning a proposal into work. Adapt the depth to the user's request.

## Establish the scope

- Identify what the user wants to decide and what is already settled.
- Read available code, documents, and examples before asking for discoverable facts.
- Distinguish current behavior from proposed behavior. A difference may be the
  purpose of the change, rather than an error in the user's description.
- Use this process when an interview is requested. A request to check a decision
  can often be answered by investigation without starting a question sequence.

## Ask useful questions

1. Identify unresolved choices that materially affect the outcome, constraints,
   public contracts, data, security, cost, or reversibility.
2. Ask a small group of questions whose answers can be decided now. Resolve a
   prerequisite before asking questions that depend on it.
3. Give a recommendation when the evidence supports one. Explain the meaningful
   trade-off and allow the user to supply a different answer.
4. Update the decision summary as answers arrive. Do not re-ask settled questions
   unless new evidence changes their consequences.

Make routine decisions independently when the user delegates them. State
assumptions that affect the result. Ask rather than assume when a choice changes
the requested outcome or crosses an authorization boundary.

Challenge vague requirements with concrete scenarios: what should happen when
only part of an order ships, a request is repeated, or access is revoked?
Use scenarios relevant to the proposal; do not enumerate speculative edge cases.
Offer your best-supported recommendation, not one designed to provoke rejection.

## Conclude when the important decisions are clear

Summarize:

- the outcome, intended users, and evidence of success;
- constraints, decisions, and the reasons that matter;
- deliberate exclusions;
- remaining questions, their consequences, and which work they block.

Accept clear agreement or explicit delegation in context. Request confirmation
only where a consequential decision remains unresolved. Do not require a
particular confirmation phrase.

An interview alone does not authorize implementation. If the user already
authorized implementation after resolving these questions, continue within that
scope. Otherwise deliver the decisions and recommended next action.

If interaction is unavailable, record unresolved questions and their impact.
Treat only questions that prevent a correct next action as blockers; complete
independent work that remains authorized.

## Verification

- [ ] Questions addressed material uncertainty rather than discoverable facts.
- [ ] Recommendations followed the evidence and respected explicit delegation.
- [ ] Settled decisions, exclusions, and consequential assumptions are recorded.
- [ ] Remaining questions identify the work they block.
- [ ] The next action stays within the user's authorization.
