# Evaluation and operations

Choose evidence that can change a design or release decision. Reuse existing
checks before building a separate evaluation stack. Measure task outcomes and
consequential failures, then use component evidence to locate their causes.

## Build a useful evaluation set

1. Define the user outcome and the cost of failure. Distinguish a wrong answer,
   unsupported claim, unnecessary abstention, unauthorized effect, and incomplete
   task; one composite average can hide a critical failure.
2. Collect representative requests and failure cases from permitted sources.
   Preserve the facts and constraints that make each case meaningful. Use
   minimized or synthetic data where privacy requires it, and state how that
   limits representativeness.
3. Label the expected outcome and supporting evidence independently of the
   system's answer. Record acceptable alternatives and when no answer is possible.
   A generated reference answer is a labeling candidate, not automatic truth.
4. Separate prompt/model tuning examples from held-out assessment. For production
   regressions, preserve a case that fails on the old defect rather than merely
   matching the repaired implementation's wording.
5. Group results by materially different task or failure types. A small diagnostic
   set can choose a direction, but cannot establish rare-failure rates or broad
   production safety. Choose coverage and repetitions from the decision's risk.

An illustrative case shape is:

```yaml
case_id: trial_cancel_04
request: What cancellation period applies to a trial account?
fixture: permitted current policy revision and authenticated account type
expected_outcome: answer the trial period with supporting evidence
required_evidence: current trial-policy row
acceptable_alternatives: explain missing evidence if the fixture omits that row
forbidden_effects: reads of another tenant's private material
```

The fixture, expected outcome, and grader belong to the evaluator's controlled
materials. Keep hidden expected answers out of the evaluated agent's context and
readable files, and protect acceptance graders from modification. Agents may edit
project tests when the task calls for it; those edits must not redefine the
protected acceptance checks. Expose task requirements and useful feedback without
leaking answers. Isolate trials from shared writable caches/history that could
transfer solutions between them.

## Make comparisons interpretable

Compare baseline and candidate on the same tasks, relevant data, tools, and
operating conditions. Record model/prompt versions, generation settings, tool
contracts, corpus/index or memory state, and evaluator configuration. Pin model
snapshots/settings where supported and record effective model identity when
exposed. Pinning does not guarantee deterministic outputs or an unchanged service.

Repeat stochastic trials when their variability could change the decision. A
paired comparison can reveal which cases improved or regressed; an aggregate
mean alone conceals that. Record failed or timed-out trials instead of silently
rerunning until success. Reuse evidence only when the change cannot affect its
inputs, execution, or interpretation.

When evaluating guidance itself, distinguish whether it was available, loaded,
applied, and beneficial. Compare matched tasks with the current and changed
instructions; a no-skill comparison can test whether either adds value. Keep the
model, tools, and case facts comparable, define the scoring before seeing results,
and do not reveal the desired answer in the request. More detailed output or
repetition of the guidance's vocabulary is not itself an improvement.

## Replay recorded responses to test the application

A recorded model response replayed through the application's real entry point
tests the code around the model, such as prompt assembly, tool wiring, state,
and effects, without model variance or provider cost. It shows whether the
application still behaves as it did under those responses, not whether a live
model would still give them: a change to prompts, tools, or models that could
alter the model's choices needs live trials as well.

- Record from a live run, then replay through the launcher or configuration the
  product ships, in a disposable workspace, with requests to the provider
  disabled or failing loudly.
- When the claim concerns prompt assembly or tool wiring, compare each request
  the application sends with the recorded one before returning its response,
  on the fields that claim depends on, such as the assembled instructions, the
  tool definitions, and the order of calls. A regression can change any of
  them while consuming the same number of responses; recorded prompt and tool
  definitions kept beside the recording help only where the check compares
  them with what the application actually sent.
- Fail the replay when the application makes more requests than the recording
  holds or leaves a recorded response unused, so an ignored response fails
  instead of passing silently.
- Assert effects apart from the model's narrative. Compare the final workspace
  or external state with an expected state kept separately from the recording,
  and a read-only case with its starting state; a response saying a file was
  written shows nothing about the file.
- Re-record deliberately when an intended change alters the requests, and
  review the new recording and the expected state separately; never regenerate
  the expected state from a replay.
- Normalize only values outside the contract, such as generated identifiers and
  timestamps, and keep credentials and personal data out of recordings.

## Grade facts and outcomes with appropriate oracles

| Surface | Evidence and oracle |
|---|---|
| Structured output | Schema plus domain constraints; valid JSON alone is insufficient. |
| Retrieval | Labeled supporting evidence and stage traces; distinguish relevance recall from ANN accuracy. |
| Grounded answers | Claim support, correctness, relevance, completeness, citation accuracy, and appropriate abstention. |
| Memory | Extraction precision/completeness, correct subject/scope, update behavior, recall, and later task outcome. |
| Tool workflows | Executor records and final environment state, including forbidden or duplicated effects. |
| User experience | Whether users complete the task, understand uncertainty, and can recover or escalate. |

Prefer deterministic checks where they establish the fact: numerical results,
permitted identifiers, schema constraints, or service/database state. A model's
claim to have created a record is not proof that it exists. Likewise, a citation
is not proof that the cited passage supports the answer.

### Worked rubric: a fluent answer with the wrong evidence

Suppose a supplied policy says trial customers have 7 days and paid customers
have 30 days. The question is about a trial customer. A useful rubric separates:

| Criterion | What to inspect |
|---|---|
| Correctness | Does the answer apply the trial rule to the stated account? |
| Evidence support | Does the cited region support that rule and its qualifications? |
| Relevance/completeness | Does it answer the period and any condition material to the request? |
| Appropriate abstention | Is the needed evidence actually missing or conflicting? |

"You have 30 days" with a citation to the paid-plan row fails even though the
number occurs in the source and the prose is clear. "Trial customers have 7 days"
with the trial row can pass in different wording. "I don't know" is appropriate
if the relevant evidence is genuinely unavailable; the same phrase is an omission
when the fixture provides it. Lexical overlap and abstention phrases must not
assign correctness or faithfulness automatically.

For model grading, supply the request, permitted evidence, response, and criterion
being judged. Validate references against source evidence; do not reward matching
a mistaken gold answer. Use human-reviewed correct and plausible wrong examples
to calibrate. In pairwise grading, test swapped answer order and inspect style,
length, and model-family preferences rather than assuming their absence.
[MT-Bench judge research](https://arxiv.org/abs/2306.05685) studies these biases;
its findings are not fixed failure rates for current judges.

## Check whether a second judge fixes the first one's errors

A more expensive judge is not automatically independent. Evaluate a proposed
cascade on human-labeled cases from both accepted and rejected/escalated groups,
including confident first-judge mistakes. Inspect false accepts, false rejects,
and error overlap by criterion. If strata are sampled at different rates, account
for that before estimating a production-wide rate.

For example, both judges may accept the wrong trial answer because both follow
a mistaken reference. Escalating only low-confidence answers misses their shared
confident error. A deterministic policy check, corrected labels, or expert review
may help more than another judge call. [Rubric-judge comparisons](https://arxiv.org/abs/2609.29769)
provide empirical examples; a paper's judge rankings or savings are not evidence
for your own cascade.

For consequential release scores, report sample uncertainty and judge calibration
limits. Statistical adjustment can be useful where those decisions justify it;
confidence intervals do not guarantee that a release gate never blocks a good
change or misses a regression. Avoid a new statistical subsystem for a decision
that existing focused checks can establish.

## Distinguish eventual success from consistent success

For repeated trials of one task, `pass@k` asks whether at least one of k attempts
succeeds; `pass^k` asks whether all k succeed. Aggregate over tasks deliberately,
and retain the number and conditions of trials. [Tau-bench](https://arxiv.org/html/2406.12045v1)
uses this distinction to examine reliability.

For illustration only, if independent attempts each succeed with probability
0.8, four chances give `1 - (1 - 0.8)^4 = 0.9984` probability of some success,
but `0.8^4 = 0.4096` probability of all succeeding. Real tasks and retries may
have correlated outcomes; measure trials instead of assuming that model.

A retry-rich demo can therefore look strong while ordinary single-attempt use is
inconsistent. Report first-attempt success, completion under the allowed retry
policy, relevant consistency, and total cost. Low repeated-run consistency does
not itself diagnose poor recovery; inspect the actual failed operations.

## Capture traces that establish the path and its coverage

Retain enough correlation to connect the task to retrieval, model calls, memory
updates, tools, and results. An illustrative trace can include:

```text
request/run ID; caller/scope reference; model/prompt/tool/representation versions
stage and parent span; start/end time; actual outcome and failure stage
source/result/operation locators; usage categories; retries and cost attribution
context transformations applied before a call, such as truncation or compaction
```

When prompt assembly, truncation, or a resumed session could explain a failure,
keep enough to reconstruct what the model received: the instruction and
tool-definition versions, the retrieved inputs, and each transformation applied
to the context.

Prefer locators and redacted/sampled payloads when full content is unnecessary.
Do not log credentials, hidden reasoning, or unrestricted customer material for
debugging convenience. Bound trace access and retention. Executor evidence and
agent-authored narrative must remain distinguishable.

Verify instrumentation through the actual client path with a controlled canary
where appropriate. Reconcile observed request/usage counts with an independent
counter. If spans and reported tokens fall after an instrumentation change while
provider usage stays steady, first investigate missing telemetry rather than
claiming an optimization. Check sampling rates, collector refusals, export
failures, and queues. [OpenTelemetry internal telemetry](https://opentelemetry.io/docs/collector/internal-telemetry/)
provides examples of those signals; no universal daily schedule or discrepancy
threshold follows from it.

## Budget the whole task and realistic traffic

Measure time to first useful output and total completion time, including tail
latency under expected concurrency. Streaming changes perceived progress without
necessarily shortening completion. Include ingestion, embeddings, search,
reranking, uncached/cached input, billed output/reasoning, retries, tools, storage,
evaluation, and human handling where applicable. Verify how billing categories
are counted so visible output and billed reasoning are not counted twice.

Report cost per completed task together with total spend, failures, traffic mix,
and escalation rate. Cheap calls can produce expensive loops; excluding hard
failed tasks can also make the apparent average misleading. Model the workload
before choosing batching, self-hosted inference, or an additional routing layer.

For shared/external services, enforce request, concurrency, and spend limits at
the appropriate user/tenant boundary using controls the agent cannot modify or
bypass. Bound expensive inputs and operations, monitor abuse, and explain exhausted
limits and recovery behavior to callers. A per-call cap alone does not bound a
task that starts unlimited calls.
[OWASP Unbounded Consumption](https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/)
identifies this resource-abuse risk.

## Evaluate cache reuse rather than assuming savings

Separate prefix/KV computation reuse from caching generated answers. For a
prefix of P tokens reused for n requests within a valid cache interval, a simple
input-only comparison is:

```text
without reuse: n * P * I
with reuse:   P * W + (n - 1) * P * R
```

Here I, W, and R are comparable all-in uncached, write, and read rates per token.
If a provider quotes a write surcharge, include the base cost in W rather than
counting it twice. Add storage/time charges and actual misses; repeated writes
after expiry or prefix changes can erase the apparent benefit. Caching does not
make those input tokens disappear from the model's context limit.

Keep stable content before changing request material where the API permits it.
A timestamp near the prefix start, reordered tools, or changed effort/settings
may destroy reuse. Verify actual matching/invalidation rules and usage counters
against the current provider documentation. [Prompt caching documentation](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)
is one provider example, not a portable API contract.

Compression also has a cost and can drop negation, exact values, or source
relationships. Compare uncompressed cached context, compressed cold context,
and compressed context after its own cache warms. A one-time prefix rewrite may
lose existing hits yet save cost later; neither "compress everything" nor "never
compress a stable prefix" is generally justified. Measure task quality as well
as total cost/latency before adopting it.

For cached answers, bind identity or validation to relevant access scope,
source/policy version, model/prompt, and other inputs that affect correctness.
Semantic similarity alone cannot authorize sharing. The same question can have
different answers for different tenants, account types, or policy revisions.
Invalidate or revalidate after source updates, forgetting, and access revocation.

## Check failures, fallback, and release changes

Choose cases from actual trust boundaries: cross-scope reads/writes, poisoned
sources or memory, prompt injection, unsafe generated arguments, changed access,
deleted sources, unavailable services, partial effects, cancellation, and
exhausted limits. Enforce permissions in code/service boundaries; prompts,
retrieval, fine-tuning, and content filters do not establish authorization.
[OWASP Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
describes why external content must remain untrusted.

A fallback model/provider needs compatible tools, evidence, permissions, data
handling, output format, and continuation state. Degrade explicitly when a
required dependency is missing; do not silently replace grounded answers with
unsupported generation or repeat uncertain external effects.

Rerun affected evaluations after model, prompt, representation, memory-policy,
tool, or dependency changes. Monitor quality shifts without a corresponding
release of your own, including changes behind floating model aliases. Use staged
exposure and rollback where warranted, accounting for persisted state and index
compatibility as well as code. Turn consequential production failures into
minimized reproducible regressions using permitted data.

Keep proposals, offline evaluation, integration proof, and live operation distinct.
A small suite does not prove production quality or safety. State scenarios,
environment, uncertainty, and untested paths. [Agent evaluation guidance](https://www.anthropic.com/research/demystifying-evals-for-ai-agents)
provides broader task/trial/grader examples without prescribing a universal stack.
