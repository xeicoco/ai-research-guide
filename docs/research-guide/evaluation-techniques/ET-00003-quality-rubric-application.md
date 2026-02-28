# ET-00003: Quality Rubric Application

> **Part of the [Evaluation Techniques Catalog](README.md)**

**Technique name:** Quality Rubric Application

**Purpose:** Systematically score a research answer against the five quality dimensions defined in the guide, producing a structured report that identifies specific passages for improvement.

---

## Description and Rationale

Quality Rubric Application provides a formal scoring procedure for the five-dimensional quality framework in [`research-quality-guidelines.md`](../research-quality-guidelines.md). Unlike subjective holistic review, this technique requires the evaluator to produce an explicit score (1–5) and a specific justification for each dimension before making any revision decision.

**Why this technique works:** Rubric-based evaluation reduces inter-rater variability, ensures all dimensions are considered, and produces actionable feedback tied to specific text passages. It creates an auditable evaluation record.

**Applicable to:** AI self-evaluation, automated pipelines, human peer review, developer benchmarking, community quality assurance.

---

## Evaluation Rubric

| Dimension | 1 (Poor) | 3 (Acceptable) | 5 (Excellent) |
|-----------|----------|----------------|---------------|
| **Relevance** | Off-topic or misses the question | Mostly on-topic, minor drift | Directly and completely addresses the question |
| **Depth** | Surface-level or too vague | Covers key points | Thorough, with nuance and detail |
| **Evidence** | No sources; claims unsupported | Some attribution | All major claims sourced or hedged appropriately |
| **Structure** | Hard to follow | Logical but basic | Clear, well-organized, appropriate length |
| **Uncertainty** | No hedging on uncertain claims | Some uncertainty flagged | Accurate uncertainty representation throughout |

---

## Algorithm

**Input:** A research question Q and a draft answer A.

**Output:** A structured evaluation report R and a revised answer A′ (if overall_score < 4 or any s(D) < 3).

```
Algorithm: Quality Rubric Application

1. READ Q and A.

2. FOR EACH dimension D in [Relevance, Depth, Evidence, Structure, Uncertainty]:
   a. IDENTIFY the specific passages in A relevant to D.
   b. SCORE: assign s(D) ∈ {1, 2, 3, 4, 5} using the rubric above.
   c. JUSTIFY: write one specific sentence explaining s(D), citing
      a passage from A (e.g., "Line 3 claims X without a source → Evidence = 2").

3. COMPUTE:
   overall_score = mean(s(D) for D in all dimensions)
   min_score     = min(s(D) for D in all dimensions)

4. BUILD report R = {
     scores:         {D: s(D)},
     justifications: {D: justification(D)},
     overall_score:  overall_score,
     min_score:      min_score,
     action:         "APPROVE" if overall_score ≥ 4.0 AND min_score ≥ 3
                     else "REVISE"
   }

5. IF action == "REVISE":
   FOR EACH D where s(D) < 3:
     a. LOCATE the specific passage(s) in A causing the low score.
     b. REWRITE the passage(s) to address the identified deficiency.
     c. UPDATE s(D) after revision.
   REPEAT steps 3–4 until action == "APPROVE" or a maximum of 3 revision cycles.

6. RETURN R and A′.
```

---

## Dual Implementation

### 🤖 AI Instance (Real-Time Application)

Apply the rubric as an internal checklist before finalizing any research response:

1. Score each dimension on a 1–5 scale with a one-sentence justification.
2. If any dimension scores below 3, identify the specific weakness and revise.
3. Output the revised answer. Optionally, append the scores if the user has asked for quality transparency.

**Compact self-check format:**
```
Relevance: [score]/5 — [one sentence justification]
Depth:     [score]/5 — [one sentence justification]
Evidence:  [score]/5 — [one sentence justification]
Structure: [score]/5 — [one sentence justification]
Uncertainty: [score]/5 — [one sentence justification]
→ [APPROVE / REVISE: list dimensions to improve]
```

### ⚙️ Developer / AI Operator Implementation

1. **Post-generation eval step:** After primary answer generation, run a rubric scoring call using the structured format above.
2. **Feedback loop:** If any dimension < 3, append the critique to the context and regenerate.
3. **Logging:** Store rubric scores per query for quality monitoring and regression detection.
4. **Threshold tuning:** Adjust the approval threshold (default: overall ≥ 4.0, min ≥ 3) based on use case — stricter for medical/legal contexts, more lenient for casual Q&A.

### 👤 Human Researcher / Reviewer Application

1. After completing a draft, apply the rubric table manually.
2. Record a score and brief justification for each dimension.
3. Use the scores to prioritize revision effort (lowest scores first).
4. Re-score after revision to confirm improvement.

---

## Example

**Research question:** "What is the difference between supervised and unsupervised learning?"

**Draft answer:** "Supervised learning uses labeled data. Unsupervised learning does not have labels. Both are types of machine learning."

**Rubric application:**

| Dimension | Score | Justification |
|-----------|-------|---------------|
| Relevance | 3 | Addresses the core distinction but misses nuance (semi-supervised, self-supervised). |
| Depth | 1 | Three sentences with no examples, no mechanisms, no use cases. |
| Evidence | 2 | No citations; claims are accurate but unsupported. |
| Structure | 2 | No organization; needs subsections or contrast structure. |
| Uncertainty | 4 | No false certainty; the claims made are well-established. |

**Overall:** 2.4/5 → REVISE (Depth = 1, Structure = 2 below threshold)

**Revision focus:** Expand Depth (add mechanism, examples, use cases), improve Structure (use clear contrast format or table).

---

## References

- Bloom, B. S. (1956). *Taxonomy of Educational Objectives.* — foundational rubric framework.
- Palomba, C. A. & Banta, T. W. (1999). *Assessment Essentials.* Jossey-Bass.
- OpenAI (2023). "GPT-4 Technical Report." — discussion of evaluation criteria for LLM outputs.
