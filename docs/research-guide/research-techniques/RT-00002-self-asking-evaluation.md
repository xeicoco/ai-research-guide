# RT-00002: Self-Asking Evaluation

> **Part of the [Research Techniques Catalog](README.md)**

**Technique name:** Self-Asking Evaluation

**Purpose:** Evaluate and improve research answers by decomposing the original question into sub-questions, verifying that each sub-question is answered, and identifying gaps before finalizing output.

---

## Description and Rationale

Self-Asking Evaluation adapts the Self-Ask prompting technique (Press et al., 2022) to the evaluation domain. The evaluator explicitly generates the set of sub-questions that a complete answer to the research question must address, then checks whether the draft answer covers each one.

**Why this technique works:** Complex research questions implicitly require answers to multiple sub-questions. Draft answers often miss one or more sub-questions without the author noticing. Making sub-questions explicit surfaces these gaps before output.

**Applicable to:** AI self-evaluation, structured research workflows, systematic reviews, question decomposition for RAG pipelines.

---

## Evaluation Criteria Reference

This technique specifically strengthens:

| Dimension | How Self-Asking Helps |
|-----------|-----------------------|
| **Relevance** | Confirms that all aspects of the question are addressed |
| **Depth** | Identifies which sub-questions require more detail |
| **Evidence** | Prompts sourcing for each factual sub-claim |
| **Uncertainty** | Identifies which sub-questions have contested or unknown answers |

---

## Algorithm

**Input:** A research question Q and a draft answer A.

**Output:** A gap analysis report and a revised answer A′ (if needed).

```
Algorithm: Self-Asking Evaluation

1. READ Q (the original research question).

2. DECOMPOSE Q into sub-questions:
   a. Ask: "To fully answer Q, what must I know or explain?"
   b. Generate SQ = {SQ₁, SQ₂, ..., SQₙ} — a complete set of sub-questions
      such that answering all SQᵢ is sufficient to answer Q.
   c. Verify: Is there any aspect of Q not covered by SQ?
      If yes, add missing sub-questions.

3. FOR EACH SQᵢ in SQ:
   a. SEARCH A for a passage that answers SQᵢ.
   b. IF found: Mark SQᵢ as covered. Note if the answer is superficial.
   c. IF NOT found: Mark SQᵢ as MISSING.

4. FOR EACH SQᵢ marked MISSING:
   a. GENERATE an answer to SQᵢ.
   b. INSERT the answer into A at the appropriate location.

5. FOR EACH SQᵢ marked as superficially covered:
   a. EXPAND the existing passage to provide adequate depth.

6. RETURN A′ (revised answer with all sub-questions covered).
```

---

## Dual Implementation

### 🤖 AI Instance (Real-Time Application)

Before returning a research answer:

1. Re-read the question and ask: *"What are all the sub-questions this question is really asking?"*
2. List the sub-questions explicitly.
3. For each sub-question, check your draft: *"Did I answer this?"*
4. If any sub-question is unanswered or shallow, revise before outputting.

**Example (internal self-ask):**
```
Question: "What are the risks and benefits of CRISPR gene editing in agriculture?"

Sub-questions I must answer:
1. What is CRISPR gene editing? (context)
2. What are the agricultural applications? (scope)
3. What are the documented benefits? (benefits)
4. What are the documented risks? (risks — biological, environmental, social)
5. What is the current regulatory status? (context + uncertainty)
6. Are these risks contested or well-established? (uncertainty)

→ Review draft and ensure all 6 are covered.
```

### ⚙️ Developer / AI Operator Implementation

1. **Two-step pipeline:**
   - Step 1: Generate sub-questions from Q via a dedicated decomposition call.
   - Step 2: For each sub-question, retrieve relevant context and verify coverage in the draft answer.
2. **RAG integration:** Use generated sub-questions as individual retrieval queries to improve recall.
3. **Coverage check:** After generation, run a verification call: *"Does the following answer address each of these sub-questions? List any gaps."*

### 👤 Human Researcher / Reviewer Application

1. Before writing, list all sub-questions that the research question implies.
2. Write or review the answer with each sub-question as a separate checklist item.
3. Before submission, verify each sub-question has an explicit corresponding passage.
4. If a sub-question cannot be answered (e.g., unknown or contested), acknowledge this explicitly in the answer.

---

## Example

**Research question:** "How does the EU AI Act classify AI systems by risk?"

**Sub-questions generated:**
1. What are the risk categories defined in the EU AI Act?
2. What criteria determine each category?
3. What are examples of systems in each category?
4. What obligations apply to each category?
5. Are there any contested or evolving aspects of this classification?

**Gap check on a draft answer that only describes "high-risk" and "unacceptable risk" categories:**
- SQ1: partially covered (missing "limited risk" and "minimal risk")
- SQ2: not covered
- SQ3: partially covered
- SQ4: not covered
- SQ5: not covered

**Result:** 3 gaps identified → draft revised to cover all categories, criteria, obligations, and knowledge cutoff caveat.

---

## References

- Press, O., et al. (2022). "Measuring and Narrowing the Compositionality Gap in Language Models." *EMNLP 2023.*
- Gao, L., et al. (2023). "Precise Zero-Shot Dense Retrieval without Relevance Labels." *ACL 2023.*
