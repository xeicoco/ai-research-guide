# RT-00005: Iterative Research Questioning

> **Part of the [Research Techniques Catalog](README.md)**

**Technique name:** Iterative Research Questioning

**Purpose:** Systematically advance understanding of a research topic by identifying the current knowledge state, detecting the highest-value knowledge gap, formulating the next question, and repeating until the research goal is satisfied.

---

## Description and Rationale

Iterative Research Questioning formalizes the natural scientific process of progressive inquiry: each research cycle produces new knowledge that in turn reveals new gaps, which drive the next question. Rather than attempting to answer a complex topic in one pass, this technique treats research as a sequence of focused questions, each informed by the cumulative results of prior cycles.

**Why this technique works:** Single-pass research on complex topics routinely misses important dimensions because the researcher cannot simultaneously identify all gaps before beginning. By making knowledge-state assessment an explicit step before each question, this technique ensures that each new question is the most valuable one given what is already known. This prevents both redundant effort (asking already-answered questions) and premature closure (declaring research complete before key gaps are filled).

**Applicable to:** AI research agents conducting multi-turn investigations, systematic review workflows, developer-implemented progressive research pipelines, and human researchers structuring a research session with AI tools.

---

## Evaluation Criteria Reference

This technique strengthens all five quality dimensions through its iterative structure:

| Dimension | How Iterative Research Questioning Helps |
|-----------|------------------------------------------|
| **Relevance** | Each question is explicitly evaluated against the research goal before being asked |
| **Depth** | Iterating until gaps are filled ensures no dimension is superficially addressed |
| **Evidence** | Each cycle produces evidence that is explicitly integrated into the knowledge state |
| **Structure** | Knowledge state accumulates in a structured form, making the final answer well-organized |
| **Uncertainty** | Unresolvable gaps are explicitly identified and flagged as remaining uncertainties |

---

## Algorithm

**Input:** A research goal G (the overarching question or topic to be understood) and an initial knowledge state K₀ (which may be empty or partially populated).

**Output:** A final knowledge state K_final that satisfies G, plus a list of unresolved gaps U.

```
Algorithm: Iterative Research Questioning

INITIALIZATION

1. SET K = K₀  (current knowledge state; initially empty or seeded)
2. SET U = {}  (set of unresolvable gaps)
3. SET cycle = 0

MAIN LOOP

4. REPEAT:

   a. cycle = cycle + 1

   b. ASSESS CURRENT KNOWLEDGE STATE:
      - LIST all facts, claims, and relationships currently in K.
      - NOTE the source and confidence level of each item.

   c. IDENTIFY KNOWLEDGE GAPS:
      - For each sub-dimension of G (What? Why? How? When? Who? Where?),
        ask: "Is this sub-dimension fully covered in K?"
      - Generate gap list GL = {gap₁, gap₂, ..., gapₙ} where each gapᵢ
        is a specific missing piece of knowledge required to satisfy G.

   d. IF GL is empty:
      BREAK  (research goal G is satisfied; proceed to step 9)

   e. PRIORITIZE GAPS:
      For each gapᵢ in GL, estimate:
        - Research value v(gapᵢ): How much does filling this gap advance G?
        - Answerability a(gapᵢ): Is this gap answerable with available sources?
      SET next_gap = argmax v(gapᵢ) among gaps where a(gapᵢ) > 0

   f. IF no gap has a(gapᵢ) > 0:
      - MOVE all remaining gaps to U (unresolvable with available sources).
      BREAK

   g. FORMULATE NEXT QUESTION:
      - Translate next_gap into a precise, answerable research question Q_next.
      - Verify: Is Q_next specific enough to produce a useful answer?
        If not, narrow the scope.
      - Verify: Is Q_next already answered in K?
        If yes, mark the gap as resolved and return to step 4c.

   h. EXECUTE Q_next:
      - Submit Q_next to the research source (AI, database, literature, search).
      - Receive answer A_next.

   i. INTEGRATE RESULTS:
      - Extract all new facts, claims, and relationships from A_next.
      - Add each to K with its source and confidence level.
      - Remove next_gap from GL.

   j. EVALUATE CYCLE QUALITY:
      - Apply RT-00001 (CoT Self-Evaluation) to A_next.
      - If any quality dimension < 3, re-query with a refined question
        before proceeding.

5. UNTIL GL is empty OR no answerable gaps remain OR cycle ≥ MAX_CYCLES

CONCLUSION

6. SYNTHESIZE K into a coherent answer A_final that satisfies G.
7. FLAG all items in U as unresolved uncertainties in A_final.
8. RETURN A_final and U.
```

---

## Dual Implementation

### 🤖 AI Instance (Real-Time Application)

When tasked with a complex research question that cannot be fully answered in one pass:

1. **State your current knowledge explicitly** before each iteration: "Here is what I currently know about X: [list]."
2. **Identify what you don't know**: "The following aspects are not yet covered: [list gaps]."
3. **Ask yourself the highest-value next question**: "The most important gap to fill next is: [gap] → my next question is: [Q_next]."
4. **Answer the next question**, integrate the result, and repeat.
5. **Stop when all gaps are filled** or explicitly flag remaining gaps as unresolvable given your training data or context.

**Example internal iteration prompt:**
```
Research goal: "Understand the causes and effects of the 2008 financial crisis."

Cycle 1:
- Known: The crisis involved mortgage-backed securities and bank failures.
- Gaps: (1) root causes of MBS risk mispricing, (2) regulatory failures,
         (3) transmission to real economy, (4) policy responses, (5) long-term effects.
- Highest-value gap: root causes (foundational).
- Next question: "What caused mortgage-backed securities to be systematically mispriced before 2008?"
→ Answer → integrate → cycle 2.
```

### ⚙️ Developer / AI Operator Implementation

1. **State machine design:** Implement the algorithm as a state machine with states: `ASSESS → IDENTIFY_GAPS → PRIORITIZE → FORMULATE → EXECUTE → INTEGRATE → EVALUATE → ASSESS`.
2. **Knowledge state representation:** Store K as a structured object (e.g., JSON with fields: `fact`, `source`, `confidence`, `cycle_added`).
3. **Gap prioritization:** Score gaps on two axes — research value (how central to the goal) and answerability (does the model have access to relevant information). Use a simple weighted score: `priority = α * value + (1-α) * answerability`.
4. **Termination conditions:** Implement hard limits (max cycles, max token budget) alongside the natural termination condition (empty gap list).
5. **Quality gate:** After each cycle, run an RT-00001 scoring call. If `min(scores) < 3`, trigger a re-query before advancing.
6. **Synthesis step:** After the loop, run a dedicated synthesis call that converts K into a coherent narrative answer, explicitly marking items in U as open questions.

### 👤 Human Researcher Application

1. **Start with a knowledge inventory:** Before your research session, write down everything you already know about the topic.
2. **List your gaps explicitly:** For each major sub-dimension of your research goal, note what you don't know.
3. **Rank your gaps:** Which gap, if filled, would most advance your understanding? Start there.
4. **Ask one question at a time:** Resist the temptation to ask a broad question. Narrow it to the specific gap.
5. **Integrate before asking the next question:** After receiving an answer, update your knowledge list and re-identify gaps.
6. **Track unresolvable gaps:** If a gap cannot be filled with available sources, note it explicitly as an open question in your final output.

---

## Example

**Research goal:** "Understand how transformer neural networks achieve attention."

**Cycle 1:**
- Known: Transformers are a type of neural network used in language models.
- Gaps: (1) mechanism of attention, (2) role of Q/K/V matrices, (3) multi-head attention, (4) positional encoding, (5) why transformers outperform RNNs.
- Highest-value gap: mechanism of attention (foundational to all others).
- Next question: "How does the self-attention mechanism in transformers compute attention weights?"
- Answer integrated: Self-attention computes dot products between query and key vectors, applies softmax to get weights, then takes a weighted sum of value vectors. K updated.

**Cycle 2:**
- Known: + self-attention mechanism (Q·Kᵀ / √d_k → softmax → weighted sum of V).
- Gaps remaining: (2) role of Q/K/V matrices, (3) multi-head attention, (4) positional encoding, (5) RNN comparison.
- Next gap: role of Q/K/V matrices (directly builds on cycle 1 result).
- Next question: "What do the query, key, and value matrices represent in transformer attention, and how are they learned?"
- Answer integrated. K updated.

**[Cycles 3–5 continue for multi-head attention, positional encoding, RNN comparison.]**

**Final output:** A structured explanation of transformer attention covering all five sub-dimensions, with a flagged uncertainty: "The intuitive interpretation of what individual attention heads learn remains an active research question (Jain & Wallace, 2019)."

---

## References

[1] Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. *Advances in Neural Information Processing Systems*, 30. https://arxiv.org/abs/1706.03762

[2] Kuhn, T. S. (1962). *The Structure of Scientific Revolutions.* University of Chicago Press. — foundational account of knowledge-gap-driven scientific progress.

[3] Higgins, J. P. T., & Green, S. (Eds.). (2011). *Cochrane Handbook for Systematic Reviews of Interventions* (Version 5.1.0). The Cochrane Collaboration. https://handbook.cochrane.org — systematic review methodology formalizing iterative question refinement.

[4] Jain, S., & Wallace, B. C. (2019). Attention is not explanation. *Proceedings of NAACL-HLT 2019*, 3543–3556. https://aclanthology.org/N19-1357/

[5] Press, O., Zhang, M., Min, S., Schmidt, L., Smith, N. A., & Lewis, M. (2023). Measuring and narrowing the compositionality gap in language models. *Findings of EMNLP 2023*. https://arxiv.org/abs/2210.03350 — decomposition-driven iterative querying.

[6] Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. *ICLR 2023*. https://arxiv.org/abs/2210.03629 — iterative reason-act cycles for research tasks.
