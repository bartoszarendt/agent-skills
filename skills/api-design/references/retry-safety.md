# Retry safety

Use this reference for operations that can be repeated by callers, queues,
workers, or recovery tools. Focus on effects that would cause harm if duplicated.

## Define the operation

Identify the intent, its caller, its authorization scope, and its side effects.
Choose whether repetition should return an existing result, perform an equivalent
operation, or be rejected. Document that behavior.

An idempotency key identifies one intent, not one attempt. Reuse it across retries
of that intent and use a distinct key for a new intent. A timestamp or new UUID
generated for every attempt defeats deduplication. A key based only on user and
amount can collapse legitimate repeated purchases.

Scope keys to the relevant tenant, caller, and operation. Authorize retrieval
and replay of stored results as well as initial execution.

## Claim and record

Use an atomic uniqueness mechanism or equivalent conditional write to claim the
intent before applying its effect. A separate "not found" check followed by an
insert does not prevent concurrent execution.

Store a canonical payload fingerprint and reject reuse of a key with a different
request. Define what an in-flight duplicate receives: a bounded wait, a pending
result, or a retryable conflict. Do not let a second worker through merely
because the first appears slow.

Persist enough state to distinguish success, known failure, and unknown outcome.
A timeout does not establish that the effect failed.

## Handle external effects

A local uniqueness constraint cannot make a remote effect and local result write
one transaction. If the provider succeeds and the worker crashes before recording
the result, recovery must not blindly repeat the effect.

Use the provider's retry contract with the same stable intent key where supported.
Otherwise define reconciliation, a queryable operation identifier, or a manual
resolution path. Keep unknown outcomes explicit until evidence resolves them.
Do not present a local or mocked check as proof of provider behavior.

Bound waiting and retries. Preserve the claim during uncertain outcomes rather
than expiring it into a new execution. Recovery ownership needs evidence that
the earlier worker can no longer apply the effect or that repetition is safe.

## Retention and verification

Set retention from the longest supported redelivery or replay path, including
operator replays and delayed queues. State what happens to retries after expiry.

Verify the risks the contract actually carries:

- overlapping requests produce at most the permitted number of effects;
- one key with a different payload is rejected;
- replay does not expose another caller's result;
- a crash after the effect but before result storage remains reconcilable;
- timeout and known failure are not conflated;
- retention covers the documented replay window.

Use existing cases where sufficient, and choose the lowest-cost boundary that
can establish each claim. Live-provider checks require authorization for their
effects and cost.
