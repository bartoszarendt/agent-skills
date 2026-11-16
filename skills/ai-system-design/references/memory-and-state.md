# Memory and state

Design memory around a future task it should improve. Establish permitted
retention, owner, scope, and correction behavior before choosing storage. Compare
with current context and simple retrieval over permitted history. More retained
information can increase errors as well as cost.

## Choose what must survive

| Responsibility | Example | Consequential failure |
|---|---|---|
| Working context | Current request and selected tool results | Compaction drops a constraint needed for the next action. |
| Execution state | Pending operation and confirmed results | A resumed run repeats an effect whose outcome was unknown. |
| Episodic evidence | What happened in an earlier interaction | A summary keeps values but loses who, why, or under which conditions. |
| Facts and preferences | A scoped preference or observation | An obsolete fact is retrieved as current, or another person's fact is attributed to the user. |
| Procedures | Deliberately maintained operating instructions | An untrusted memory becomes instructions for every later task. |

These are responsibilities, not mandatory stores. Files suit small, navigable,
reviewable material; relational records suit exact updates and constraints;
semantic search suits fuzzy recall; graphs help when relationship queries earn
their maintenance cost. A vector index is a retrieval representation, and a
prompt/KV cache reuses computation. Neither establishes application truth.

## Represent assertions without losing their subject or time

For consequential facts, retain a way to explain the assertion and replace it.
The following is an illustrative record, not a required schema:

```yaml
memory_id: m18
scope: {tenant: example_org, user: u7}
subject: user:u7
attribute: home_city
value: Berlin
assertion_kind: stated
source_ref: conversation:c4/turn:19
recorded_at: 2026-11-10T09:00:00Z
retired_at: null
valid_from: 2026-11-01
valid_to: null
supersedes: m11
```

Here the user reported on November 10 that they moved on November 1. Real-world
validity and system knowledge have different timelines. "Where did they live on
November 5?" differs from "What did we know on November 5?" If both questions
matter, preserve historical records and when each entered or left the system's
accepted view; overwriting the value loses that distinction.

Include only fields the use case needs. Source locators must respect retention
and access scope; a locator to deleted evidence cannot establish its contents.
Mark direct statements, observations, and inferences distinctly. A confidence
number is useful only if its meaning and calibration support a decision.

## Extract and update deliberately

1. Resolve the subject, attribute, scope, and relevant time from the source.
   "My friend is vegetarian" does not assert a diet for the speaker. Quoted,
   hypothetical, negated, and temporary statements need their qualifiers.
2. Decide whether retaining it serves an authorized future use. Do not persist
   incidental information about third parties simply because it can be extracted.
3. Validate write scope outside the model. A generated user or tenant identifier
   must not choose which person's records the writer can modify.
4. Compare with the same subject and attribute in the relevant scope. Semantic
   similarity finds candidates; it does not establish that two facts are equal.
   "Avoid overnight flights" and "Prefer overnight flights" are close in wording.
5. Apply the appropriate update, preserving evidence and invalidating affected
   summaries/index entries. Use a transaction or version check where concurrent
   writers could overwrite a correction or create contradictory current facts.

| New information | Appropriate interpretation |
|---|---|
| "That earlier address was a mistake" | Correction: reject or supersede the mistaken assertion; preserve history only if required and permitted. |
| "I moved last week" | Temporal change: close the old validity interval and open the new one. |
| "For this trip, use trains" | Temporary override: attach it to the trip; do not replace the general preference. |
| Two sources disagree without enough context | Unresolved contradiction: retain the distinction or ask; do not silently promote one claim. |

Authority depends on the attribute and the source's competence. A user's account
may control a preference, while an authenticated account service controls a
payment's status. Do not impose one universal ordering of users, tools, and
inferences. Repetition or recent retrieval does not independently verify a fact.

An obsolete fact should cease being current through correction or supersession.
Merely lowering its recency score allows it to resurface when a query changes.

## Choose when to curate

Extraction and consolidation discard detail. Select their timing according to
read latency, future-task predictability, and permitted access to source history.

| Timing | Useful when | Failure or cost to test |
|---|---|---|
| Write time | Future lookups are predictable and reads must be fast | An extractor commits to an interpretation before the later question exists. |
| Background | Consolidation can be delayed and spread across requests | Readers see stale or partially rebuilt views; concurrent corrections can be overwritten. |
| Read time | The same history supports different future tasks | Retrieval plus task-conditioned curation adds latency and per-read cost. |

For example, an earlier purchase interaction may supply product preferences for
a shopping task and a navigation sequence for an interface task. One fixed
summary need not preserve both. Task-conditioned curation can retrieve source
episodes and construct the needed view at read time. [Just-in-Time Memory](https://arxiv.org/html/2609.27334v1)
studies this approach; its results do not justify retaining all transcripts or
moving every memory operation onto the request path.

## Diagnose lost information before changing retrieval

Hold the question, reader, and relevant permissions constant. Compare:

1. Retrieval over permitted source messages or episodes.
2. Retrieval over the extracted or consolidated memory.
3. The complete relevant transformed memory, bypassing its retriever where it
   fits within a comparable usable context budget.

If source evidence succeeds but even the complete transformed memory fails,
inspect what extraction removed. If complete transformed memory succeeds while
retrieval over it fails, investigate lookup, ranking, and context selection.
If known-good evidence is present and the reader still fails, investigate the
reader's reasoning or instructions. These are diagnostic comparisons, not proof
of one unique cause; inspect the differing evidence and context lengths.

Example: a summary retains "Maya - Berlin" but loses whether Berlin was her
destination, connection airport, or rejected option. A better vector index cannot
reconstruct that missing relationship. [Raw-RAG research](https://arxiv.org/html/2610.30755v1)
shows this kind of information-loss problem on conversation benchmarks. It
supports keeping a raw-history baseline and loss checks, not a universal claim
that extracted facts or graphs are inferior.

## Separate retrieval from influence on the current task

After retrieving candidates, decide which are useful in the current scope.
Accurate recall can still bias the answer toward an old task's conditions.

For example, a past exercise forbade network access. Recalling that exercise
accurately does not make the restriction applicable to a new request explicitly
requiring live verification. Supply the episode as historical evidence only if
it helps, rather than promoting its instructions into the current task.

Compare task outcomes with candidate memories included versus withheld. Inspect
irrelevant constraints, reasoning fixation, and obsolete assumptions as well as
missing recall. [MemTrapBench](https://arxiv.org/html/2608.20202v1) investigates such
failure modes on deliberately challenging tasks; it does not establish that
ordinary personalization is generally harmful or that all tested memories were
true. Allow a request to use no persistent memory.

## Worked preference update

Suppose an assistant has authorized user-scoped preference retention:

1. "My colleague is vegetarian. I prefer email for routine updates." Extract a
   preference for the user about routine updates. Do not assign the colleague's
   diet to the user or retain it without a relevant purpose.
2. "Use SMS for billing updates this month." Add a billing-specific temporary
   override with an explicit validity boundary. Keep the routine-email preference.
3. Before a billing notification, match the subject, purpose, scope, and current
   validity. The override does not authorize sending a notification; the action
   still needs the application's existing permissions and user intent.
4. After expiry, stop applying the override. A semantic match on "billing" must
   not revive it. A later permanent change is a separate update, not an extension
   silently inferred from the expired record.
5. If the user requests forgetting, remove or retire the relevant retained data
   according to that request and the system's retention obligations. Invalidate
   derived summaries, embeddings, and cached decisions so the preference is not
   recreated from a stale copy.

This example needs scope and validity rules, not a dedicated graph database.
For large derived stores, keep enough lineage to find affected records; account
for backups and version history under the retention policy rather than promising
that deleting one visible row removes every retained copy immediately.

## Check compaction as a transformation

Before compacting, identify the current goal, explicit restrictions and decisions,
unresolved work, source locators, and confirmed or unknown operation outcomes.
After compacting, compare those items and perform the next meaningful task using
the compacted state. Check meaning, not merely how many facts survived.

"Prepare a deletion plan; do not execute it" becoming "prepare and execute
deletion" is a material failure. Likewise, a timed-out payment must not become
"payment failed" or "payment succeeded" in a summary. Preserve the uncertainty
and reconcile it from the operation's evidence before retrying.

Prefer removing expendable tool output or retaining locators where that keeps
the needed evidence without rewriting decision-bearing context. Keep source
history only within authorized retention. Do not require access to hidden model
reasoning or treat a model-written summary as new authority. [Context engineering](https://www.anthropic.com/research/effective-context-engineering-for-ai-agents)
describes compaction and structured notes; verify any provider-specific state
preservation mechanism against its current documentation.

## Evaluate the operation that can fail

Use multi-turn cases where the final question genuinely needs earlier evidence.
Assess extraction precision and completeness, correct subject/scope attribution,
update correctness, retrieval quality, and downstream task outcomes separately.
An extractor that writes nothing avoids false assertions but fails useful recall.
[HaluMem](https://aclanthology.org/2026.emnlp-main.220/) provides operation-level
memory evaluation examples; avoid adopting its system rankings as your own result.

Include the consequential cases the system supports: a correction, retroactive
change, temporary override, contradiction, forgotten fact, different user's
record, or concurrent update. Measure the effect of memory on quality, latency,
and cost against the simpler baseline. Do not count a faithful repetition of a
wrong memory as a correct answer.

For context/memory separation and external storage, [MemGPT](https://arxiv.org/abs/2310.08560)
is a foundational example, not a required hierarchy or storage architecture.
