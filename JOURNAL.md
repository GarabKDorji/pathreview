## Week 7 — Issue selection

**Issue link:** [https://github.com/ascherj/pathreview/issues/24]

**Issue title:** Hybrid retriever over-weights keyword results when query contains technology names

**Tier:** [ ] Tier 1  [✓] Tier 2  [ ] Tier 3

**Problem summary:**
The hybrid retriever currently combines vector similarity and BM25 keyword scores using fixed equal weights. When a query includes common technology names such as Python or React, keyword matches can receive too much importance and return chunks from the wrong document. This issue affects the scoring logic in rag/retriever/hybrid.py. A successful fix should improve the weighting strategy so that relevant semantic matches are ranked above unrelated chunks that only share technology keywords.


**Branch name:** [fix/24-hybrid-retriever-keyword-weighting]

**Setup confirmation:** [✓] App runs locally at localhost:5173

**Cohort ledger:** [✓] Issue added to cohort ledger


## Week 8 — Reproduction & solution planning

**Reproduction commit link:** (https://github.com/GarabKDorji/pathreview/commit/141b3e433788faa8f0b9371a66f1c3ca4a49cecb)

**Reproduction summary:**
I reproduced the hybrid-retriever ranking issue by adding unit tests in tests/unit/test_hybrid.py. The failing tests show that a keyword-only result, or a weaker vector result with a strong BM25 boost, can outrank a more semantically relevant vector result.

**PLAN.md link:** (https://github.com/GarabKDorji/pathreview/blob/fix/24-hybrid-retriever-keyword-weighting/PLAN.md)

**Walkthrough video (recommended):** https://drive.google.com/file/d/1PTOnbrvv-nu3mmv85VzRiT0O8M7N_fPp/view?usp=sharing

**Blockers or open questions:**
I still need to determine which score-combination strategy is the most appropriate. I plan to compare Weighted Reciprocal Rank Fusion, BM25 score saturation or capping, and reducing the keyword contribution for chunks with weak or missing vector relevance. I also need to confirm why the issue description refers to equal weights when the current implementation defaults to 0.7 vector weight and 0.3 keyword weight.