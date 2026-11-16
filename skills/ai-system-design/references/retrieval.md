# Retrieval and grounded generation

Design ingestion and query-time retrieval together. Start with the queries users
need to answer, the evidence that would support them, and who may access it.
Keep a plain baseline while investigating the stage that actually fails.

## Choose the baseline from the question

Point lookup, semantic discovery, comparison, and exhaustive aggregation need
different evidence. Query structured facts directly where appropriate. Top-k
similarity search does not establish that every contract or every invoice was
examined; use a coverage-preserving query or scan for exhaustive questions.

For a small permitted corpus, compare direct context with retrieval. For example,
a public handbook may fit comfortably in the usable context window and need no
index. Compare answer quality, update frequency, latency, and actual reuse of
cached context. Document count alone is not a decision rule: a few long scanned
documents can be harder than many short pages.

For repeated requests, `corpus_tokens × cache_read_rate` versus
`retrieved_tokens × input_rate` is only a cached-corpus/uncached-retrieval input
estimate. Include actual hit rates on both paths, writes and rebuilds, search,
embedding and reranking costs, and measured latency. A shared context must be
permitted for every user who receives it; separate access scopes where necessary.

## Keep retrieval representations linked to source evidence

The following groups illustrate useful metadata, not a required storage schema:

| Identity or lineage | What it enables |
|---|---|
| `source_id`, `source_revision` | Identify which original changed, was deleted, or supports the answer. |
| `block_id`, `chunk_id`, `parent_id` where used | Reassemble context and invalidate affected derivatives. |
| Page/section/row locator and, for visual documents, bounding box | Open the actual cited evidence instead of a generated summary. |
| Trusted tenant/access scope and relevant policy identity | Search within the permitted material and recheck current access. |
| Parser, chunking, preprocessing, and embedding-space identity | Explain why representations differ and determine what needs rebuilding. |

Trace the actual path:

```text
source version -> parsed blocks -> retrieval units/proxies -> candidate search
               -> fusion/reranking -> context selection -> answer -> citations
```

Inspect representative parsed output before tuning embeddings. A two-column
statement can preserve every word while assigning an amount to the wrong year.
For layout-sensitive documents, preserve typed text/table/image blocks, reading
order, page/region provenance, and labels needed to interpret values. [Docling's
document model](https://docling-project.github.io/docling/reference/docling_document/)
illustrates these structures without requiring that parser.

A caption, table summary, or generated question may be an effective retrieval
proxy. For exact values or visual relationships, follow its link to the original
table, validated cells, or page region before answering. "Revenue increased"
can find a chart but cannot support a specific quarterly percentage. Direct
page-image retrieval is another option when layout carries the evidence;
[ColPali](https://arxiv.org/abs/2407.01449) explores that approach.

Preserve meaningful differences during deduplication. Policies differing only in
"7 days" versus "30 days" can look almost identical. Similarity does not establish
that one can replace the other. Choose canonical versions deliberately while
retaining the permissions and provenance the application needs.

## Repair missing chunk context at the appropriate stage

| Mechanism | What changes | What it does not repair by itself |
|---|---|---|
| Parent-document expansion | Retrieve a small child, then supply its surrounding/parent evidence | A child that never matched because its product name was absent. |
| Contextual text prefix | Add document identity or explanation to each unit before dense and lexical indexing | A wrong generated prefix, which can make false context more retrievable. |
| Late chunking | Encode the longer document before pooling token spans into chunk vectors | Missing terms in a separate lexical index, or evidence beyond the encoder's usable context. |

Example: a chunk says "It costs $200" while the product name appears only in a
heading. Expanding its parent helps the reader after retrieval. Adding the heading
to indexed text can help both keyword and dense retrieval. Late chunking changes
the dense representation; bare BM25 still does not see the missing name.
[Contextual Retrieval](https://www.anthropic.com/research/contextual-retrieval) and
[Late Chunking](https://arxiv.org/abs/2409.04701) describe different remedies.

Split along useful structure and preserve units, headings, table labels, and
source boundaries. Use observed errors to vary retrieval-unit size, overlap,
and returned context. Fixed token sizes are experiment settings, not universal
production defaults. Do not stack all three remedies without measuring benefit.

## Retrieve and combine candidates deliberately

Use lexical retrieval for names, identifiers, and exact terms; dense retrieval
for semantic similarity; hybrid retrieval where queries need both. Test on the
actual language and domain. Rewrite conversational queries only while preserving
constraints, identifiers, negation, and the user's intended question.

Raw keyword and vector scores need not share a scale. Reciprocal rank fusion
combines rankings without assuming their scores are comparable:

```text
rrf_score(d) = sum over result lists containing d of 1 / (c + rank_i(d))
```

Ranks start at 1; an absent item contributes nothing. `c` controls how strongly
rank differences matter and is distinct from the candidate count. Fuse consistent
identities: decide whether an item is a chunk or a document. RRF is a useful
baseline; calibrated score fusion or learned ranking can be better on a given
workload. [Elastic's RRF documentation](https://www.elastic.co/docs/reference/elasticsearch/rest-apis/reciprocal-rank-fusion)
provides an explicit implementation example.

A reranker can reorder a bounded candidate set but cannot recover an item absent
from that set. First check candidate recall; then measure whether reranking puts
useful evidence into the final context. Graph traversal or staged retrieval may
help connected questions, while exhaustive aggregation still needs a coverage
contract. Adaptive search needs evidence of benefit and bounded extra calls.

## Apply permissions without starving the candidate set

Derive tenant and access scope from trusted authentication. A global top-k
followed only by tenant filtering can return too few results even when the tenant
has relevant documents. Search within an appropriate partition or use supported
filter-aware retrieval; measure filtered recall for selective tenants. Exact
search over a small eligible subset may be a useful comparison.

Do not turn this into a blanket rule that every post-filter is wrong. Retrieval
engines differ in how they over-collect or apply filters. The required properties
are adequate permitted candidates and no unauthorized content reaching the reader,
reranker, or other external service. Revalidate current access where stale indexes
or caches could expose revoked material. [Elastic kNN filtering](https://www.elastic.co/docs/reference/query-languages/query-dsl/query-dsl-knn-query)
explains one engine's pre-filter/post-filter behavior.

## Diagnose a wrong answer with stage-specific evidence

Use the same query, eligible corpus, representation, and reader configuration
while changing one relevant stage. Preserve source locations in diagnostic traces.

| Check | Diagnostic experiment | Likely next investigation |
|---|---|---|
| Did the source contain the answer? | Open the authoritative revision and region | Source coverage, freshness, or a legitimate no-answer case. |
| Did parsing preserve it? | Compare parsed blocks with the visible source | OCR, reading order, tables, or parser changes. |
| Did indexing retain the needed relationship? | Inspect the indexed unit and its metadata | Chunk boundaries, missing headings, wrong summaries, or stale versions. |
| Does exact vector search rank useful evidence? | Exact search on the same eligible vectors plus human relevance labels | Embedding suitability, query formulation, or representation quality. |
| Does approximate search reproduce exact neighbors? | Compare ANN results with exact kNN under the same filters | Search breadth, quantization, indexing, or filter interaction. |
| Did fusion/reranking/context selection retain it? | Follow candidate IDs through each stage | Ranking, duplicates, token budget, or truncation. |
| Can the reader answer from known-good evidence? | Supply supporting source material directly, without the expected answer | Reader behavior, instructions, reasoning, or conflicting evidence. |
| Does each citation support the claim? | Resolve cited locations and inspect the claim's support | Wrong locator, unsupported synthesis, or a false source. |

Verify that the approximate-search comparison exercised an actual built ANN index;
an exact fallback for small or unindexed segments can produce perfect overlap
without testing approximation quality.

For example, useful evidence ranked third by exact search but absent from ANN
results suggests an approximation/index issue. It does not establish that the
embedder is ideal. If known-good evidence is present yet the answer is wrong,
further expanding search may only add noise.

## Define what the retrieval metric measures

Separate these two meanings of recall:

- **Relevance recall@k:** relevant labeled items retrieved in the first k divided
  by all relevant labeled items for the query. Its denominator depends on the
  completeness of the relevance judgments.
- **ANN recall@k:** overlap between approximate and exact nearest-neighbor sets,
  relative to the exact set being compared. Exact neighbors are not automatically
  useful evidence. Hold the corpus, eligible scope, vectors, metric, and k constant.

For fixed-cutoff precision@k, divide the relevant items among the first k by k;
missing result positions contribute no relevant items. Returning two relevant
items for k=10 gives P@10=0.2, not 1. If measuring precision over returned items
instead, name that convention and report the returned count. [NIST's implementation](https://github.com/usnistgov/trec_eval/blob/main/m_P.c)
makes the fixed-cutoff convention explicit.

Use MRR for how early the first relevant item appears and nDCG when graded
relevance and its rank discount fit the task. MRR cannot show that all evidence
for a comparison was found. No-answer queries need separate answerability and
abstention evaluation; do not divide recall by zero or silently drop those queries
from every report.

For example, if A and C are the relevant documents and the results are A then B,
recall@2 and precision@2 are both 1/2, while reciprocal rank is 1. Finding an
excellent first passage does not establish that the comparison evidence C was
found. MRR averages reciprocal rank over queries, with missing relevant results
contributing zero. A common graded form is
`DCG@k = sum((2^relevance_i - 1) / log2(i + 1))`; nDCG divides by the ideal DCG
under the same judgments. Define label grades and zero-ideal handling explicitly.

Label at the unit being scored. For document-level evaluation, deduplicate the
ordered chunk results by document before assigning document ranks. If document A
has chunks at ranks 1 and 8, a map overwritten by the later chunk can incorrectly
place A below document B at rank 2. Keep the first occurrence when aggregating.
For chunk-level evaluation, label the relevant passages instead. Record which
units were judged; unjudged evidence is not automatically irrelevant.

[Qdrant's ANN recall guide](https://qdrant.tech/documentation/tutorials-search-engineering/ann-recall/)
and [retrieval relevance guide](https://qdrant.tech/documentation/search-evaluation/retrieval-relevance/)
make these distinctions concrete. Their thresholds or example datasets are not
acceptance targets for a new application.

## Worked multi-tenant policy search

Suppose two organizations share an index. The authenticated user belongs to A;
A's current trial policy says 7 days, its older policy says 30 days, and B has a
similarly titled policy. The question asks about A's trial cancellation period.

1. Resolve A's permitted current source version before content reaches a model.
   Filtering a small global candidate set after search may leave none from A.
2. Inspect the source and parser output. If a table lost its "trial" column label,
   changing top-k will not distinguish the trial and paid-plan periods.
3. If the heading was dropped from chunks, compare contextual indexing or parent
   expansion according to where evidence disappeared. Do not simply add a graph.
4. Inspect exact versus approximate retrieval, then reranking and final context.
   Remove superseded duplicates while retaining the current source locator.
5. Generate the trial answer and cite the supporting region. "30 days" with a
   citation to the paid-plan row is still wrong, even if the number appears in
   an authorized document. If the current trial evidence is missing, report that
   limitation rather than supplying the older or other tenant's policy.

Add update, revocation, no-answer, and malicious-document cases when those paths
matter. For web/open corpora, evaluate source authority as well as relevance.
Verify consequential contact details, payment links, and login URLs against
primary sources; use curated sources or allowlists when the risk warrants it.
Never infer a destination solely from its plausible appearance.

## Change representations as a migration when consequences warrant it

Matching dimensions do not establish a compatible embedding space. Track the
query/document encoder pair and relevant preprocessing. Explicitly compatible
asymmetric encoders can differ; an arbitrary model/version swap is not equivalent.

For a consequential large index, a possible sequence is: create a new
representation, arrange safe update propagation, backfill, shadow-query the same
tasks, compare relevance and performance, cut over, and retain a viable rollback
route. Handle deletes and access revocation during the backfill too. A small
rebuild may need none of that parallel machinery.

Finally check answer correctness, grounded support, relevance/completeness, and
citation accuracy separately. A faithful answer may repeat a false source, and
a relevant answer may omit a crucial qualification. [Foundational RAG](https://arxiv.org/abs/2005.11401)
and [Lost in the Middle](https://arxiv.org/abs/2307.03172) are useful background;
neither establishes that retrieved evidence will be complete or fully used.
