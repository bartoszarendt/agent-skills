# Agents and workflows

Choose control flow from uncertainty in the task. A workflow follows steps
selected by code; an agent lets a model choose subsequent actions from
observations. Both can use tools, retrieval, and memory. Persistent memory,
multiple agents, and a graph runtime are not prerequisites for useful tool use.

## Choose the control that the task needs

| Task shape | Starting design | Reason to expand |
|---|---|---|
| Bounded transformation or classification | A direct call with a validated result | Specific failures need evidence, tools, or additional reasoning. |
| Known dependencies and branches | An explicit workflow | Observations require routes that fixed branches handle poorly. |
| Search or actions whose next step depends on results | A bounded adaptive loop | Measured task completion warrants its extra calls and failure paths. |
| Independent work or extensive intermediate context | Parallel work or focused subagents | Better quality, elapsed time, permissions, or context isolation outweigh coordination. |

For an adaptive loop, make the boundary concrete: observe current state, select
a permitted operation, validate its arguments/preconditions, execute, observe the
result, and decide whether the actual outcome is complete. A model's statement
that a task is finished is an observation to check, not the completion oracle.

A framework is useful when its persistence, control flow, integrations, or
instrumentation solve a current problem. Account for its state model, replay
semantics, and debugging/operations cost before adopting it.

## Define tool behavior, not just a JSON schema

Describe purpose, inputs, trusted context, outputs, side effects, caller-handled
errors, and retry behavior. Here is a design sketch for a wrapper, not a claim
that any issue-tracker API already supplies these semantics:

```yaml
operation: create_issue
arguments:
  project_id: permitted project identifier
  summary: short issue title
trusted_context:
  tenant_id: derived from authenticated caller
  actor_id: derived from authenticated caller
  intent_id: stable identifier for one accepted create request
success:
  issue_id: identifier confirmed by the service
  result_ref: location the caller can verify
other_outcomes:
  invalid_request: no effect; correct the arguments
  forbidden: no effect; do not retry with broader access
  pending: accepted but not yet complete
  unknown: effect may have committed; reconcile before repeating
retry_contract: same intent and payload replays the original outcome if supported
```

Enforce scope and domain invariants outside the model. The generated project ID
must not bypass authorization. Validate inputs before execution and distinguish
schema validity from a permitted operation. Expose only capabilities the task
needs, with bounded outputs and useful identifiers rather than unrestricted data.

An intent ID identifies one requested effect; an attempt ID identifies one try.
Keep the intent stable across retries. A new UUID per attempt defeats downstream
deduplication; a key based only on title/project can collapse two deliberately
separate issues. Reject reuse of an intent with a different payload where the
service contract requires it. Authorize replay/result lookup as well as creation.
Check downstream key scope and retention; replay beyond its deduplication window
may require reconciliation rather than another create call.

A tool protocol such as MCP standardizes integration, not these guarantees.
Check current protocol, provider, and wrapper behavior before relying on retries,
identity propagation, or result formats.

## Check private data, untrusted content, and outbound access together

An agent that can read private data, encounter untrusted content, and send data
out has an exfiltration path to examine. Where practical, remove one capability
while processing untrusted content: use an environment without private data or
outbound access, then pass only task data validated against a narrow contract.
A summary or another agent sharing the same context and capabilities does not
create that boundary.

Enforce permitted destinations and payloads in application/service controls.
Remote-image loading, link previews, uploads, and messages are outbound effects
too. Do not automatically fetch untrusted or generated URLs without applying
those controls. Content cannot authorize a new recipient or disclosure; ask only
when the existing user authorization does not cover the data and destination.

For example, a support ticket tells an assistant to embed an external image with
a private customer record in its URL. Rendering the image can send that record
without any email tool. Treat the ticket as data and prevent the unapproved fetch;
merely summarizing its instruction does not authorize the disclosure.

## Record the execution evidence at a trustworthy boundary

For consequential tools, retain enough executor/service evidence to distinguish
what was proposed, attempted, and confirmed. A possible record contains:

```text
intent_id, attempt_id, actual_tool, canonical_target, payload_fingerprint
actor/scope reference, relevant authorization/artifact reference
started_at, ended_at, execution_outcome, failure_stage, remote_operation_id
result_ref
```

Fields depend on the operation; do not create a separate log store when existing
service records establish the outcome. Protect access and retention, and redact
payloads rather than logging secrets. A model-authored narrative or an agent's
own "success" flag cannot replace executor or environment evidence.

For batches, distinguish steps that failed from steps that were never executed.
For asynchronous work, "accepted" is not "completed." Keep an operation locator
so the caller can determine the eventual result.

## Recover according to what is known

| Observed outcome | Response |
|---|---|
| Arguments rejected before execution | Correct the request; do not repeat it unchanged. |
| Transient read/service failure with safe repetition | Use bounded retry/backoff under the actual service contract. |
| Forbidden operation | Report the boundary; do not search for a credential or tool that evades it. |
| Side effect may have committed | Reconcile by stable operation/intent identity, or replay under verified downstream idempotency. |
| Later step skipped after a failure | Report not executed; decide whether its preconditions now hold. |
| Cancellation during an external call | Preserve uncertainty until evidence establishes whether the effect happened. |

A local uniqueness constraint cannot atomically commit a remote effect and a
local result. A crash can occur after the effect but before its receipt is stored.
A saved result helps once recorded; it does not close the preceding crash window.
A durable workflow engine cannot guarantee exactly-once arbitrary external
behavior without cooperation at the effect boundary. [Temporal's activity model](https://docs.temporal.io/activity-definition)
and [idempotency explanation](https://temporal.io/blog/idempotency-and-durable-execution)
illustrate why replay and external effects need separate reasoning.

## Worked interruption: create an issue, then notify

Suppose an authorized request should create one issue and then notify its owner:

1. Accept the intent and assign `create-41`. A worker calls the downstream service
   using that identity where its documented contract supports it.
2. The service creates issue `I-9`; the response is lost and the worker crashes
   before saving a local result. Local status is unknown, not a known failure.
3. On resume, use the original operation identity to reconcile or replay under
   the service's idempotency contract. Do not generate a new create intent simply
   because there is no local success receipt.
4. Confirm `I-9` from service/executor evidence and record the result. Only then
   execute the notification if it remains requested and permitted. If notification
   had already been attempted, reconcile that effect separately.
5. Report the actual states. A summary saying "issue created and owner notified"
   cannot establish either effect. A checkpoint before the create step does not
   undo the existing issue.

If the downstream service has no reliable deduplication or lookup mechanism,
retain the uncertain outcome and use the supported resolution path. Automatically
retrying may be unacceptable. A deliberate request for a separate additional
effect is a new intent even if its content resembles an earlier one. A retry of
the original intended effect retains its identity; a new message alone does not
establish a new intent.

Verify this contract around the crash window, not only on a clean success path.
Check final issue count and notification state at their actual owning services.
A local mock cannot prove the remote provider honors the claimed contract.

## Bind consequential authorization to the effect

Define what existing authorization covers and which changed conditions need a
new decision. Apply the check at the action boundary; do not add approvals for
every read or repeat approval while its relevant conditions still hold.

For example, an operator approves `python maintenance.py`, then the file changes
before execution. Binding approval only to the command string permits different
behavior. Where artifact identity matters, bind verification to the content
actually executed using an immutable snapshot, mutation fence, or equivalent
execution binding. Hashing a file and then reopening its mutable path leaves a
check/use race. Verify relevant targets/preconditions too. Follow the effect
through subprocesses and delegated tools; a top-level argument hash does not
establish what mutable dependencies actually do.

[Approval Laundering](https://arxiv.org/abs/2609.38983) studies divergences below an
approval boundary. It supports checking the connection between review and effect,
not mandating signed tokens, universal expiry, or per-call human review.
Permissions, isolation, and service invariants still apply after approval.

## Bound work and define progress semantically

Choose deadlines, spend, concurrency, and tool-call/retry limits from the workload
and consequence. Enforce consequential budgets and stop conditions in
executor/service controls the agent cannot modify or bypass; use existing runtime
controls where they provide this boundary. Make cancellation,
exhausted limits, and any recoverable partial result visible to the caller. A
textual refusal or limit message must not hide an external operation still running.

Do not identify a loop solely by identical `(tool, arguments)`. Repeating a valid
status poll may be expected while an asynchronous job progresses. Repeating an
unchanged invalid request is different. Consider the observed state/error,
expected completion signal, elapsed time, and deadline. Stop or change approach
when continued calls cannot obtain new evidence or useful progress.

Persist execution state when lost work or repeated effects are unacceptable.
Replayable workflow logic, remote effects, and compensation have different
semantics. Restoring an old checkpoint is not a rollback of a payment or email;
a compensating action is another effect with its own contract and authorization.
Short, cheap, safely repeatable work may need only a simple queue or restart.

## Preserve the right state across context and model changes

Keep canonical task state, evidence locators, tool identities/results, and
confirmed or unknown operation outcomes available independently of a provider's
wire-format transcript. Do not reconstruct hidden reasoning as application state.

A provider/model switch may not accept prior reasoning blocks, tool formats, or
continuation state. Verify the documented compatibility; re-establish an accurate
task summary or restart the relevant turn when necessary. Evaluate the fallback's
tools, permissions, evidence, data handling, and output contract. An alternate
provider is not a reason to repeat already attempted external effects.

## Use multiple agents for a demonstrated benefit

Assign independent work, different required capabilities/permissions, genuinely
independent review, or exploration whose large intermediate context can remain
isolated. Specify ownership, inputs, shared-state writes, output/source locators,
and result integration. Return useful findings without copying every tool result.
One agent's untrusted output cannot grant another additional authority.

Compare total quality, elapsed time, duplicated context, cost, and recovery against
the simpler design. Several agents agreeing is not independent verification when
they share the same mistaken source or oracle. A faster subtask can still make
the whole workflow slower or more expensive.

[Building effective agents](https://www.anthropic.com/research/building-effective-agents)
describes composable control patterns. [OWASP Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)
explains why unnecessary tools, permissions, and autonomy enlarge the failure's
impact. Use them to assess actual capabilities, not to impose one agent stack.
