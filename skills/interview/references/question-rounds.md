# Question rounds

Use this guidance when an interview involves several connected decisions. The
goal is a sequence of rounds in which each answer narrows what remains open.

## Track dependencies

Keep a working list of open decisions and, for each, the decisions or facts it
depends on. A decision is ready to ask when its prerequisites are settled.

- An answer can settle a decision, unblock others, remove a branch, or add new
  decisions the proposal did not reveal earlier.
- A pending investigation is an unsettled prerequisite. Questions that depend on
  it wait; the others proceed.
- A decision the user explicitly defers leaves the rounds. Record the deferral,
  its consequence, and the work it blocks; do not treat its branch as decided.

Keep the list in the conversation unless the user asks for a durable record.
Show it when it helps the user see what remains; do not repeat it every round.

## Choose a round

Ask every ready decision that materially affects the result. When that set is
too large to answer thoughtfully in one reply, ask first the decisions with the
most dependents or the greatest consequence, and name what follows.

Combine closely related questions only when a single answer resolves them.
Split a question when the user could reasonably answer its parts differently.

## Handle answers

- **Partial answer.** Record what was settled and ask the remainder in the next
  round, narrowed to what is still open.
- **Delegation of a decision**, such as "you decide." Choose from the evidence,
  state the choice and reason, and mark it as delegated.
- **Uncertainty or missing knowledge**, such as "I don't know." Identify
  whether the answer depends on a fact you can investigate, someone else's
  decision, or information not yet available. Offer a provisional default when
  one is safe, and record what it blocks otherwise.
- **Disagreement with a recommendation.** Accept the user's decision. If it
  carries a material consequence they may not have considered, state it once and
  ask whether it changes the answer.
- **Explicit revision.** When the user replaces an earlier answer, accept it,
  update the decisions that depended on it, and state any that reopen.
- **Answer that conflicts with a settled decision.** When it is unclear whether
  the user intends a revision, name the conflict and ask which holds before
  continuing on either branch.
- **Expanded scope.** Add an area the user explicitly brings into scope. When
  the intent is unclear, ask whether it belongs in this interview or should be
  recorded as a separate question.

## Example exchange

Proposal: add a CSV export of invoices.

Map and round 1:

```markdown
The export touches audience and permissions, the consuming system and its
column layout, volume and delivery, and filtering. The billing code already
stores invoices per customer with issue dates; nothing yet defines who exports
or where the file goes. This round settles audience and consumer, which the
other areas depend on.

**Q1. Audience.** Is the export for finance staff in the admin area, or for
customers in their accounts? This determines permissions and data volume.

Recommendation: finance staff only; customers already download invoice PDFs.

**Q2. Consumer.** Will the file be imported by an accounting system with a fixed
layout, or read by people in a spreadsheet?

Recommendation: none yet; a required import layout would fix the columns.
```

User: "Finance staff. They import it into the accounting system, but I don't
know which columns it expects."

Q1 is settled. Q2 is partly settled: the consumer is known; the layout is not.
Investigation found that a month-end export covers about 40,000 invoices.

Round 2:

```markdown
Audience is settled: finance staff in the admin area. The accounting import
leaves the column layout open and raises volume: a month-end export covers
about 40,000 invoices. This round resolves the layout source and delivery;
filtering follows once the layout is known.

**Q2. Column layout.** Can someone in finance provide a sample import file or
the system's import specification?

Recommendation: block column mapping on that sample; build filtering and
delivery meanwhile.

**Q3. Delivery.** A month-end export covers about 40,000 invoices. Generate it
within the request, or as a background job with a download link?

Recommendation: background job; existing reports already use one.
```

Q3 was not ready in round 1 because the volume depended on the audience. The
round opens with progress, follows up on the partial answer before the new
area, and keeps filtering on the map for a later round.
