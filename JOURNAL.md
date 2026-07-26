## Week 7 — Issue selection

**Issue link:** [https://github.com/ascherj/pathreview/issues/24]

**Issue title:** [paste issue title here]

**Tier:** [ ] Tier 1  [✓] Tier 2  [ ] Tier 3

**Problem summary:**
The hybrid retriever currently combines vector similarity and BM25 keyword scores using fixed equal weights. When a query includes common technology names such as Python or React, keyword matches can receive too much importance and return chunks from the wrong document. This issue affects the scoring logic in rag/retriever/hybrid.py. A successful fix should improve the weighting strategy so that relevant semantic matches are ranked above unrelated chunks that only share technology keywords.

**Branch name:** [fix/24-hybrid-retriever-keyword-weighting]

**Setup confirmation:** [✓] App runs locally at localhost:5173

**Cohort ledger:** [✓] Issue added to cohort ledger