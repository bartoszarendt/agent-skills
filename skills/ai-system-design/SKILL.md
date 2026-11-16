---
name: ai-system-design
description: Design and assess LLM-based applications and tool-using agents, including model and context strategy, RAG, memory, workflows, evaluation, and production tradeoffs. Use when choosing or revising an AI system architecture or deciding which mechanisms a use case needs; not for isolated prompt rewrites or model-training tutorials.
---

# AI System Design

Choose an architecture that meets the user outcome with evidence for its
complexity. Connect model behavior to data, application state, tools, and
operating constraints. Scale the design to the actual workload and consequence.

A design or review request authorizes analysis and recommendations. Continue
into implementation only when requested or already authorized; a design does
not itself authorize data collection, training, deployment, or external actions.

## Establish the outcome and baseline

Identify what users need to accomplish, who consumes the result, and what a
wrong answer or action would cost. Distinguish generating advice from executing
an operation. Define when the system should answer, ask, abstain, or escalate.

Inspect existing code, data sources, integrations, and representative requests
before choosing components. Establish the constraints that could change the
design: quality, latency, traffic and concurrency, cost, freshness, privacy,
tenancy, deployment environment, and recovery needs. Mark unknowns rather than
inventing targets; ask only when an unresolved requirement changes the choice.

Compare with the simplest viable baseline. Existing search, rules, ordinary
code, or a single model call may be sufficient. For an existing system, use its
observed failures to locate the gap before proposing a replacement.

## Choose mechanisms by the gap they close

These choices can coexist; none is a mandatory layer.

| Need or observed gap | Candidate approach | Evidence needed before expanding |
|---|---|---|
| Exact calculation, validation, or a known rule | Ordinary code or a database query | Show where language understanding or generation adds value. |
| A bounded language task | One model call with clear instructions, examples, and an output contract | Check representative successes and consequential failures. |
| A small, permitted body of relevant material | Supply it directly in context | Measure quality, latency, and cost as context grows. |
| Changing, selective, large, or permissioned knowledge | Retrieve evidence before generation | Measure retrieval and final answer quality separately. |
| Useful continuity across interactions | Retain scoped memory | Show improvement over current context or retrieval over retained history. |
| Known steps and tool dependencies | An explicit workflow | Identify where a fixed path fails before making control adaptive. |
| Steps depend on observations that cannot be predicted adequately | An agent with bounded tool use | Compare task completion, failure behavior, latency, and total cost. |
| Persistent behavioral or task-performance gaps with suitable training data | Fine-tuning or distillation | Compare against prompting, retrieval, and model choice on held-out tasks. |

Fine-tuning and retrieval solve different problems and can be combined. Do not
use weight updates as the default mechanism for frequently changing facts,
source attribution, or per-user access control. Consider training-data rights,
quality, leakage, update cost, and rollback before recommending adaptation.

## Select the model and compose context

Evaluate models on the application's tasks, including output format, tool use,
language, modality, reasoning needs, and failure cases. Compare quality against
latency, total task cost, availability, data handling, and operating burden.
Choose managed or self-hosted inference from those constraints; open weights
alone do not establish low cost, suitable licensing, or acceptable operation.

Use current primary documentation when a decision depends on model capabilities,
API behavior, prices, limits, or retention terms. If it is unavailable, identify
the unverified assumption and keep dependent recommendations provisional.
Do not choose a model from leaderboard position alone.

Budget context for instructions, user input, retrieved evidence, memory, tool
results, and output. Select relevant information and preserve identifiers and
source locations. Test long-context use rather than assuming that fitting in
the advertised window means the model uses all material reliably.

Load large documents, tool descriptions, or results on demand through stable
identifiers or paths when the environment supports it. Otherwise select the
relevant excerpts explicitly. Keep enough context to discover what is available
and follow evidence back to its source.

Separate trusted application instructions from user material, retrieved text,
memory, and tool output. Delimiters help interpretation; they do not enforce
authorization. Validate structured output in code, then check its domain
meaning: valid JSON does not establish a correct or permitted action.

## Design knowledge, memory, and execution

For RAG or document-grounded answers, read
[references/retrieval.md](references/retrieval.md). Cover ingestion and source
updates as well as query-time search. Use its stage-by-stage diagnostic procedure
to distinguish representation, index, ranking, context, and reader failures.
Preserve evidence and permissions through the whole path to citations.

For cross-interaction continuity, compaction, or persistent execution state,
read [references/memory-and-state.md](references/memory-and-state.md).
Use its assertion/update examples and loss-versus-retrieval experiments before
adding a more elaborate store. Evaluate whether recalled memory helps the task.
Retrieval supplies evidence for a request; memory retains selected information
across interactions. They can share infrastructure but need distinct write,
scope, correction, and deletion decisions. A cache is an optimization, and
remembered content is not automatically authoritative.

For tool-enabled applications, adaptive execution, or multiple agents, read
[references/agents-and-workflows.md](references/agents-and-workflows.md).
Make tool effects and recovery behavior explicit. A tool protocol or agent
framework does not establish authorization, safe retries, or task completion.
Use the tool-contract and interruption examples to trace actual execution evidence.

## Evaluate the whole system

Define success before optimizing the architecture. Use representative requests
and consequential failure cases to compare the baseline with proposed changes.
Inspect the resulting answers or environment state, not only the system's claim
that it succeeded. Add a component only when its benefit justifies its quality,
latency, cost, maintenance, and operational effects.

For evaluation, caching, cost or latency controls, observability, fallback, or
production readiness, read
[references/evaluation-and-operations.md](references/evaluation-and-operations.md).
Use its case construction, worked rubric, and judge-error analysis to choose
evidence that can change a decision; examples are not mandatory schemas or quotas.
Include relevant isolation, freshness, injection, unavailable-service, and
partial-failure cases. Use deterministic checks where they establish the
contract; calibrate judgment-based evaluation against human-reviewed examples.

Enforce access to data and tools in application or service boundaries. Derive
identity and scope from trusted authentication, and carry them through retrieval,
memory, caches, tools, and observability. Prompt instructions and output filters
cannot substitute for those controls.

Treat timeouts, retries, cancellation, resource bounds, and recovery as design
choices for the actual workload. Introduce routing, caching, fallback providers,
or durable execution only when their benefits justify their additional semantics
and operation. Recheck quality and permissions on every alternate path.

## Present the design and its evidence

Explain the recommended data and control flow, the responsibilities of each
component, and where trusted decisions occur. Use a small diagram when it makes
the boundaries easier to understand. Keep detail proportionate to the request;
a narrow decision does not require a full architecture document.

State the baseline, consequential alternatives and tradeoffs, unresolved
assumptions, and the evidence supporting each important choice. Where uncertainty
could change the design, recommend the smallest useful experiment first. Separate
measured results from expected benefits and future verification.

## Verification

- [ ] The design addresses a concrete user outcome and consequential failures.
- [ ] Added mechanisms close an identified gap relative to a simpler baseline.
- [ ] Model, context, data, memory, and tool responsibilities are explicit where used.
- [ ] Permissions, provenance, freshness, correction, and deletion cover relevant paths.
- [ ] Evaluation checks task outcomes and relevant component and failure behavior.
- [ ] Cost, latency, recovery, assumptions, and verification gaps are stated as relevant.
