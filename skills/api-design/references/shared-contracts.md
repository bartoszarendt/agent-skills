# Contracts between separately developed sides

Use this when a provider and its consumers change or deploy separately, such as
a service and its clients, a backend and a frontend built by different people
or agents, or a published schema with outside consumers. A boundary that
changes in one atomic change and has no independent consumer needs no more than
a shared type and the module's own checks.

## One authoritative shape

- Choose the artifact that owns the shape, such as a schema, an interface
  definition, or generated types. Do not let prose documents, mock files, and
  provider code each define the same payload.
- Derive consumer types and validators from that artifact where the toolchain
  allows; otherwise check them against it.
- Shape the contract around what consumers need to do, not around a storage
  row. Exposing storage models couples consumers to internals and can force
  several calls for one task.
- Where consumers act differently on them, define what a missing field, a null
  value, and an empty value mean, and state rules that span fields, such as a
  field required only in one state.

## Check both sides against it

- Validate consumer fixtures and mocks against the contract artifact, so a mock
  cannot drift from what the provider sends.
- Validate the provider's actual serialized output, including error responses,
  empty collections, nullable fields, and conditional or flagged paths. Static
  types and casts can hide runtime mismatches, such as an identifier losing
  precision or a date changing format during serialization. Fix the
  representation where the loss occurs; converting afterwards cannot restore
  the original value.
- Each side passing its own tests does not establish compatibility. Establish
  that both pass against the same artifact.

## Plan a compatible deployment order

When both sides cannot deploy together, order the change so that every deployed
combination works: accept a new form before any side requires it, support both
forms during the transition, and remove the old form only after its consumers
have moved. State how long both forms remain supported and what consumers must
change.
