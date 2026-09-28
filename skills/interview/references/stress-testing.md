# Stress testing

Use this guidance when the user asks to be grilled or wants a proposal
scrutinized. The aim is to find where the proposal is underdetermined,
inconsistent, or fragile while the user still makes each decision.

## Probe assumptions

Identify what must be true for the proposal to work. Separate assumptions that
evidence supports from those it does not. For an unsupported assumption that
matters, ask what should happen if it is false.

## Compare alternatives

Name realistic alternatives, including an existing mechanism, a smaller change,
or no change. Ask why the proposal is preferable when the answer is not evident.
Do not invent weak alternatives to make the proposal look justified.

## Use concrete scenarios

Test boundaries with scenarios relevant to the proposal: a lifecycle transition,
repeated or concurrent requests, partial failure, revoked access, large volume,
or existing data under a new rule. Ask what should happen in each.

Select scenarios whose answer could change the design. Do not enumerate
speculative edge cases.

## Pin down vague language

When a term could mean different things, propose a precise meaning and ask
whether it is correct. For example, ask whether "account" means the customer
organization or the individual user.

When a quality is stated without a criterion, such as fast, secure, simple, or
scalable, ask for an observable condition: a latency under a stated load, a
threat that must be prevented, or a step the user must not need.

## Check claims against evidence

When the user states how something works, compare it with the code, documents,
and established terminology. Present a contradiction with its evidence, and ask
whether the difference is the intended change or a misunderstanding.

## Track consistency

Compare each answer with earlier answers. Name a conflict as soon as it appears
and resolve it before building further decisions on either side.

## Keep pressure useful

Pursue a vague or evasive answer until its practical meaning is clear or the
user explicitly defers it. Stop pressing once a decision is reasoned, even when
you would choose differently; record the trade-off the user accepted.

Challenge the proposal, not the user. Do not manufacture objections to appear
thorough.
