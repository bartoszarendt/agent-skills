---
name: interview
description: Examine a proposal, plan, or open topic through rounds of questions, recommended answers, and the user's decisions until the work can proceed without invented requirements. Use when the user asks to examine an idea through an exchange of questions and answers, such as being interviewed or grilled, asks for analysis followed by questions, or wants a proposal stress-tested through questions rather than a written assessment. Also use during other work when a material uncertainty about the user's intent, requirements, constraints, or domain knowledge cannot be resolved from available evidence and needs the user's answers.
---

# Interview

Establish enough shared understanding to carry out or evaluate the requested
work without inventing material requirements. Actively discover what is
missing, examine consequential assumptions, and follow answers into the
questions they expose. The user makes the decisions; the interview surfaces,
tests, and records them.

## Conduct an exchange

When the user asks for an interview, grilling, or question-led examination,
each response advances the exchange. Analysis and recommendations support the
questions; they do not replace them. Until the interview closes, each response
presents the current round of questions or a proposal to close and waits for the
answers. End a response only after the round's answers have arrived, the user
has dismissed the round, or its unanswered questions are written in the
conversation.

When the user asks for analysis followed by questions, use the analysis to
prepare and begin the interview. A request only to analyze, review, or
recommend is not an interview request. Ask first only the questions without
which the assessment would be wrong, then deliver it with its assumptions
stated, and offer to continue with questions when material decisions remain
open.

During other work, start an interview when a material uncertainty about the
user's intent, requirements, constraints, or domain knowledge cannot be
resolved from available evidence and would change what you do next. Scale it
to the uncertainty: a single question needs no map, progress account, or
closing proposal. Once the uncertainty is resolved, resume the original task
within its authorization without asking permission to continue.

## Prepare the first round

- Identify the outcome the interview serves: what the user wants to decide,
  build, or change, and what is already settled.
- Read available code, documents, and examples before asking for discoverable facts.
- Distinguish current behavior from proposed behavior. Code establishes what
  exists, not necessarily what the user wants; a difference may be the purpose
  of the change.
- Map the topic: the areas the outcome depends on, what the evidence settles,
  and what remains open. Include areas no one has raised when the outcome
  depends on them.

Treat a question list in project documents as input, not as the interview.
Fold it into the map: drop questions the evidence answers, sharpen vague ones,
and add what it misses. Treat questions the user supplies as starting points
unless the user limits the interview to them. Respect an explicit limit; when a
material dependency lies outside it, name it once as open rather than asking
about it. Record answers only where the user or existing authorization permits.

Investigate independently discoverable facts first. Ask the user about intent,
priorities, choices, and material facts or domain meanings unavailable from
accessible evidence. When evidence answers a candidate question, drop it and
state the established fact where it matters. When an investigation is still
running, ask the questions that do not depend on it now. If the environment supports
parallel or background investigation, use it rather than delaying the round.

When the topic spans several areas, show the map briefly before the first
round: the areas, what the evidence established, what is open, and which part
this round addresses. Keep it to what the user needs to judge the scope and
answer the questions.

When the user asks for a durable record, or the project maintains a glossary,
decision records, or a specification the interview may change, read
[references/decision-capture.md](references/decision-capture.md) before the
first round so decisions are recorded as they settle.

## Ask in rounds

Treat the topic as a set of connected decisions. Some can be decided only after
others are settled.

1. Select open decisions or missing factual explanations whose prerequisites
   are settled and that materially affect the outcome, constraints, public
   contracts, data, security, cost, or reversibility.
2. Ask them together as one round. When that set is too large to answer
   thoughtfully, ask first the decisions that others depend on.
3. Leave a question for a later round when its answer depends on a question
   still open.
4. Wait for the user's answers before continuing.

Adapt the number and depth of questions to the topic, its uncertainty and
consequences, and the user's answers. There is no fixed number of questions or
rounds: one consequential question can be a round, and a broad topic can need
many rounds.

Give each question a short title and a clear question. For choices, include
relevant options or trade-offs and a recommendation when useful. Factual
explanations need neither options nor a recommended answer. Base a recommendation
on stated evidence or a named trade-off; when the evidence does not support one,
state what the answer depends on instead. A recommendation is a proposal. A
decision is settled only when the user answers it or explicitly delegates it.
Do not answer on the user's behalf or proceed as if a recommendation were accepted.

### Present the round

Use a question tool for a round only when the current mode permits it and its
description shows that it waits for the user to submit and returns their
answers. Otherwise, or when you cannot tell, ask in the conversation. When you
use such a tool:

- Offer discrete options where the choices are clear, and place the
  recommended option first, marked as recommended.
- Keep a free-form answer available.
- When a question has no meaningful discrete options, use the tool's free-text
  input if it has one; otherwise offer concrete candidates drawn from the
  evidence, or ask it in the conversation.
- When the tool limits how many questions fit in one call, split the round
  across calls, asking prerequisites first, and reassess the remaining
  questions after each call's answers. The limit governs presentation, not the
  scope of the interview.

An acknowledgement or timeout is not an answer, and neither is a preselected
option or automatic default that the user did not submit. When a tool returns
without the user's answers, keep the answers received and ask the unanswered
questions in the conversation before ending the response. When the user
dismisses or cancels the questions, do not ask them again; note that they
remain open and wait for direction.

In the conversation, number the questions:

```markdown
**Q1. Partial shipments.** Can an order ship in several parts, or does it wait
until every item is available? Splitting ships sooner but adds per-shipment
tracking and refund handling.

Recommendation: allow partial shipments; fulfillment already groups items by
warehouse.
```

For dependency tracking, partial answers, delegation, and a multi-round example,
see [references/question-rounds.md](references/question-rounds.md).

## Continue from the answers

After each response, determine what it settles, exposes, or contradicts.

- Record settled decisions. Do not re-ask them unless new evidence changes
  their consequences.
- Investigate facts the answers make discoverable before asking about them.
- Follow up when an answer permits materially different implementations. Use a
  concrete scenario relevant to the topic to establish its practical meaning.
- Add areas and decisions the answers expose to the map.
- Accept explicit delegation: decide those choices, state each decision and its
  reason, and continue.
- Recompute the open decisions and ask the next round.

Compare each answer with the original request and with the answers, decisions,
constraints, and term meanings established throughout the interview, including
across topic areas, and with code or project documents. Accept a clear revision
of an earlier answer and update the decisions that depend on it; a position that
shifts without being clearly revised is not a revision. Otherwise, when an
apparent discrepancy materially affects the outcome and its explanation is
unclear, state both positions and their consequence, using a concrete scenario
in which they cannot both hold, then ask what explains the difference, such as
different contexts, an exception, or a revision. When one explanation is
likely, propose it as the recommended answer. Check whether the reply resolves
it; if not, ask a narrower follow-up before relying on either position. Respect
deferral or cancellation, keeping unresolved discrepancies and the work they
block explicit.

Open each later round with a short account of progress: what the answers
settled, what they exposed, and what this round resolves. Ask follow-ups on
earlier answers before moving to new areas.

When the user asks to be grilled or wants a proposal scrutinized, apply
[references/stress-testing.md](references/stress-testing.md).

## Close the interview

Continue until each material decision within scope is settled, explicitly
delegated, or explicitly deferred with its consequence recorded. A pending
investigation is not a deferral; decisions that depend on it remain open. Do not
treat your own recommendation as the user's answer, or conclude from your own
analysis that a decision is clear.

Before proposing to close, test readiness: draft the brief that the next piece
of work would start from, and list each point where you would still have to
guess. Also check the draft against the original request and the decisions as
clearly revised during the interview; treat each unresolved material conflict
as an open discrepancy, not a guess.
Answering an initial question list is not enough. Deferred decisions and
the work they block stay recorded and excluded. While a guess would materially
change the work that will proceed, ask about it in another round.

When a standalone interview meets these conditions, propose closing and list
delegated and deferred decisions. The user closes the interview and may end it
at any point. Accept clear agreement in context; do not require a particular
confirmation phrase. If the user already authorized work to follow the
interview, summarize and continue once these conditions are met, without a
separate closing confirmation.

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

- [ ] While clarification remained unresolved, necessary questions were asked and answers awaited; once resolved, the applicable closure or task-resumption rule was followed.
- [ ] When the topic spanned several areas, the first round followed a brief map; later rounds opened with progress.
- [ ] Supplied question lists shaped the map; the user's explicit limits on scope were respected.
- [ ] An interview started during other work was scaled to the uncertainty, and the task resumed afterwards.
- [ ] Questions addressed intent, priorities, choices, and material facts or domain meanings unavailable from accessible evidence; independently discoverable facts were investigated first.
- [ ] A question tool was chosen only when its description showed that it waits for and returns the user's answers; unanswered questions from a presented round, other than dismissed ones, were in the conversation when a response ended; no acknowledgement, timeout, or unsubmitted default settled a decision.
- [ ] The number of questions and rounds followed the topic, not a fixed count.
- [ ] Recommendations cited evidence or a trade-off and stayed proposals until answered or delegated.
- [ ] Vague answers received a follow-up; material discrepancies across the interview were raised with their consequence and resolved as a revision, context, or exception, delegated, or kept open with the work they block.
- [ ] The readiness test left no material guess in the work that will proceed.
- [ ] Settled, delegated, and deferred decisions are recorded with their reasons.
- [ ] Closure followed the user's decision or previously authorized continuation.
- [ ] The next action stays within the user's authorization.
