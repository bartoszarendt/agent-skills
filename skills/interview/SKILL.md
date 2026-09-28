---
name: interview
description: Examine a proposal, design, or plan through rounds of questions, recommended answers, and the user's decisions. Use when the user asks to be interviewed, grilled, or questioned about an idea, or wants a proposal stress-tested through questions rather than a written assessment.
---

# Interview

Reach a shared understanding of a proposal through an exchange of questions and
answers. The user makes the decisions; the interview surfaces, tests, and
records them.

## Conduct an exchange

When the user asks for an interview, grilling, or question-led examination,
each response advances the exchange. Analysis and recommendations support the
questions; they do not replace them. Until the interview closes, end each
response with the current round of questions or a proposal to close, then wait
for the answers.

A request to analyze, review, or recommend is not an interview request. Deliver
the assessment, and offer to continue with questions when material decisions
remain open.

## Prepare the first round

- Identify what the user wants to decide and what is already settled.
- Read available code, documents, and examples before asking for discoverable facts.
- Distinguish current behavior from proposed behavior. Code establishes what
  exists, not necessarily what the user wants; a difference may be the purpose
  of the change.
- Keep preparation brief in the response. State only the context needed to
  understand and answer the questions.

Investigate facts; ask the user about intent, priorities, and choices. When
evidence answers a candidate question, drop the question and state the
established fact where it matters. When an investigation is still running, ask
the questions that do not depend on it now. If the environment supports
parallel or background investigation, use it rather than delaying the round.

When the user asks for a durable record, or the project maintains a glossary,
decision records, or a specification the interview may change, read
[references/decision-capture.md](references/decision-capture.md) before the
first round so decisions are recorded as they settle.

## Ask in rounds

Treat the proposal as a set of connected decisions. Some can be decided only
after others are settled.

1. Select open decisions whose prerequisites are settled and that materially
   affect the outcome, constraints, public contracts, data, security, cost, or
   reversibility.
2. Ask them together as one round. When that set is too large to answer
   thoughtfully, ask first the decisions that others depend on.
3. Leave a question for a later round when its answer depends on a question
   still open.
4. Wait for the user's answers before continuing.

Number each question and give it a short title, the question, the relevant
options or trade-off, and a recommended answer:

```markdown
**Q1. Partial shipments.** Can an order ship in several parts, or does it wait
until every item is available? Splitting ships sooner but adds per-shipment
tracking and refund handling.

Recommendation: allow partial shipments; fulfillment already groups items by
warehouse.
```

Give a recommendation when the evidence supports one; otherwise state what the
answer depends on. A recommendation is a proposal. A decision is settled only
when the user answers it or explicitly delegates it. Do not answer on the
user's behalf or proceed as if a recommendation were accepted.

If a structured question tool is available, it may present a question with
discrete options; keep the recommendation visible and allow a free-form answer.
Otherwise use numbered text.

For dependency tracking, partial answers, delegation, and a multi-round example,
see [references/question-rounds.md](references/question-rounds.md).

## Continue from the answers

After each response, determine what it settles, exposes, or contradicts.

- Record settled decisions. Do not re-ask them unless new evidence changes
  their consequences.
- Follow up when an answer permits materially different implementations. Use a
  concrete scenario relevant to the proposal to establish its practical meaning.
- Accept an explicit revision of an earlier answer and update the decisions
  that depend on it. Name an unclear contradiction with earlier answers, code,
  or project documents, and ask which holds.
- Accept explicit delegation: decide those choices, state each decision and its
  reason, and continue.
- Recompute the open decisions and ask the next round.

When the user asks to be grilled or wants a proposal scrutinized, apply
[references/stress-testing.md](references/stress-testing.md).

## Close the interview

Continue until each material decision within scope is settled, explicitly
delegated, or explicitly deferred with its consequence recorded. A pending
investigation is not a deferral; decisions that depend on it remain open. Do not
treat your own recommendation as the user's answer, or conclude from your own
analysis that a decision is clear.

When a standalone interview meets these conditions, propose closing and list
delegated and deferred decisions. The user closes the interview and may end it at any point. Accept
clear agreement in context; do not require a particular confirmation phrase.
If the user already authorized work to follow the interview, summarize and
continue once these conditions are met, without a separate closing confirmation.

Summarize:

- the outcome, intended users, and evidence of success;
- decisions and the reasons that matter;
- delegated decisions and the choices made;
- deliberate exclusions;
- deferred and remaining questions, their consequences, and which work they block.

An interview alone does not authorize implementation. Previously authorized work
continues within its scope, excluding work that a deferred decision blocks.
Otherwise deliver the summary and recommended next action.

If interaction is unavailable, record the questions with their recommendations
and impact instead of answering them. Treat only questions that prevent a correct
next action as blockers; complete independent work that remains authorized.

## Verification

- [ ] Each response before closing ended with questions or a proposal to close.
- [ ] Questions addressed decisions rather than discoverable facts.
- [ ] Recommendations remained proposals until the user answered or delegated them.
- [ ] Vague or contradictory answers received a follow-up.
- [ ] Settled, delegated, and deferred decisions are recorded with their reasons.
- [ ] Closure followed the user's decision or previously authorized continuation.
- [ ] The next action stays within the user's authorization.
