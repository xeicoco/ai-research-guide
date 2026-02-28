# RT-00006: AI Chatbot Research Patterns

> **Part of the [Research Techniques Catalog](README.md)**

**Technique name:** AI Chatbot Research Patterns

**Purpose:** Survey the research approaches used by leading AI chatbots (ChatGPT/GPT-4, Claude, Gemini, Copilot/Bing), extract an algorithmic pattern from each, and synthesize a unified research algorithm that combines the best practices of all approaches.

---

## Description and Rationale

Different AI chatbot systems approach complex research queries with distinct strategies shaped by their architecture, training objectives, and design philosophy. Understanding these patterns has two practical benefits: it enables AI systems to adopt the best strategies from across approaches, and it gives developers and researchers a vocabulary for evaluating and improving research pipeline design.

This technique surveys four leading AI chatbots, extracts the algorithmic core of each approach, and synthesizes a unified algorithm that can be applied by any AI system, developer, or human researcher seeking research outputs of the highest quality.

**Why this technique works:** No single AI system's approach is optimal for all research tasks. ChatGPT/GPT-4 excels at structured decomposition; Claude excels at careful uncertainty handling and long-context synthesis; Gemini excels at grounding claims in real-time information; Copilot/Bing excels at source diversity and up-to-date retrieval. A researcher who combines these approaches systematically outperforms any single approach applied in isolation.

**Applicable to:** AI systems performing multi-step research, developers designing research pipelines, prompt engineers seeking to improve research output quality, and human researchers working alongside AI tools.

---

## Evaluation Criteria Reference

This technique strengthens all five quality dimensions by drawing on complementary strengths across chatbot approaches:

| Dimension | Approach that most strengthens it |
|-----------|-----------------------------------|
| **Relevance** | ChatGPT/GPT-4 structured decomposition ensures all aspects of the question are addressed |
| **Depth** | Claude long-context synthesis and explicit reasoning chains |
| **Evidence** | Copilot/Bing citation-heavy retrieval and source diversity |
| **Structure** | ChatGPT/GPT-4 multi-step reasoning with explicit output formatting |
| **Uncertainty** | Claude explicit uncertainty flagging and constitutional reasoning |

---

## Individual Chatbot Patterns

### Pattern A: ChatGPT / GPT-4 — Structured Decomposition with Multi-Step Reasoning

**Core approach:** GPT-4 approaches complex research questions by breaking them into a structured hierarchy of sub-problems, reasoning through each step explicitly, and flagging claims where its confidence is lower (OpenAI, 2023).

**Algorithmic pattern:**
```
Pattern A: Structured Decomposition + Multi-Step Reasoning

1. PARSE the research question to identify:
   - Core claim or question to be answered
   - Implicit sub-questions required for a complete answer
   - Any constraints (scope, audience, format)

2. DECOMPOSE into an ordered list of sub-questions SQ₁, SQ₂, ..., SQₙ
   where earlier sub-questions provide context for later ones.

3. FOR EACH SQᵢ:
   a. REASON through the answer step by step.
   b. FLAG any step where confidence is moderate or low.
   c. RECORD the answer with its confidence level.

4. SYNTHESIZE sub-answers into a unified response with:
   - Clear structure matching the decomposition
   - Explicit uncertainty markers on lower-confidence claims
   - A summary that directly addresses the original question

5. VERIFY that the synthesis addresses the original question fully.
```

**Key strengths:** Systematic coverage, explicit reasoning chains, structured output.
**Key limitations:** May over-rely on parametric knowledge without external retrieval; uncertainty flags can be inconsistent on topics at or near training cutoff.

---

### Pattern B: Claude — Constitutional Reasoning with Careful Attribution and Long-Context Synthesis

**Core approach:** Claude applies a constitutional AI framework (Bai et al., 2022) that prioritizes careful source attribution, explicit acknowledgment of uncertainty, and honest representation of the limits of its knowledge. For long documents or multi-source research, Claude synthesizes across a large context window while maintaining source traceability.

**Algorithmic pattern:**
```
Pattern B: Constitutional Reasoning + Attribution + Uncertainty Disclosure

1. RECEIVE the research question.

2. APPLY constitutional principles before answering:
   - Is this question answerable with available knowledge?
   - Are there areas where the answer is genuinely uncertain?
   - Are there multiple valid perspectives that must be represented?

3. DRAFT the answer, attributing each claim to a source or
   explicitly labeling it as general knowledge or inference.

4. FOR EACH claim in the draft:
   a. IF the claim is well-established: state it directly.
   b. IF the claim is uncertain or contested: explicitly flag it
      (e.g., "It is unclear whether...", "Some researchers argue...").
   c. IF the claim is near the training cutoff or time-sensitive:
      add a recency caveat.

5. FOR LONG-CONTEXT SYNTHESIS (multiple documents or sources):
   a. Track which source supports each claim.
   b. Identify and flag contradictions between sources.
   c. Synthesize a position that accurately represents the
      weight of evidence.

6. REVIEW the draft against constitutional principles:
   - Is every uncertain claim flagged?
   - Is the answer honest about what is not known?
   - Does the answer avoid overstating confidence?

7. RETURN the answer with explicit attribution and uncertainty disclosures.
```

**Key strengths:** Rigorous uncertainty handling, honest representation of knowledge limits, strong long-context synthesis.
**Key limitations:** May be more conservative than necessary on well-established topics; long-context synthesis can be slower.

---

### Pattern C: Gemini — Multimodal Grounding with Real-Time Factuality Verification

**Core approach:** Gemini integrates real-time search and multimodal grounding (Google DeepMind, 2023) to verify factual claims against current sources. Rather than relying solely on parametric knowledge, Gemini actively grounds answers in retrieved documents and flags where retrieved evidence contradicts or updates its prior beliefs.

**Algorithmic pattern:**
```
Pattern C: Grounded Generation + Factuality Verification

1. RECEIVE the research question Q.

2. IDENTIFY claims in Q that require:
   - Current or time-sensitive information
   - Specific factual verification (statistics, dates, names, events)
   - Multimodal evidence (if applicable)

3. RETRIEVE relevant documents/sources for each claim category.

4. FOR EACH factual claim to be made:
   a. CHECK the claim against retrieved sources.
   b. IF sources confirm the claim: state it with source reference.
   c. IF sources contradict the claim: update the claim to match sources.
   d. IF sources are inconclusive: flag the claim as unverified.

5. GENERATE the answer grounded in retrieved evidence:
   - Prefer retrieved evidence over parametric knowledge for
     time-sensitive or verifiable claims.
   - Explicitly cite or reference the sources used.

6. VERIFY factuality: re-read the answer and confirm that each
   specific claim (number, date, name, event) is grounded in a
   retrieved or well-established source.

7. FLAG any claim that could not be verified against a source.
```

**Key strengths:** Up-to-date information, active factuality verification, reduced hallucination on verifiable claims.
**Key limitations:** Dependent on search quality and source availability; may introduce retrieval biases; real-time grounding not available in all contexts.

---

### Pattern D: Copilot / Bing — Web-Grounded Search with Citation Diversity

**Core approach:** Microsoft Copilot (powered by Bing search + GPT-4) grounds every response in web-retrieved sources, produces citation-heavy answers, and prioritizes source diversity to avoid single-source bias (Microsoft, 2023). It is optimized for up-to-date retrieval and explicit attribution.

**Algorithmic pattern:**
```
Pattern D: Web-Grounded Search + Citation-Heavy Attribution + Source Diversity

1. RECEIVE the research question Q.

2. GENERATE multiple search queries from Q:
   - Core query: directly expresses the main question.
   - Perspective queries: alternative phrasings or angles.
   - Recency query: adds "recent", "2024", or relevant date range.

3. RETRIEVE results for all queries.
   - Prioritize: authoritative sources, recent publications, diversity
     of source type (academic, government, news, practitioner).

4. FOR EACH retrieved source:
   a. EXTRACT relevant claims.
   b. ASSIGN inline citation markers.

5. SYNTHESIZE answer from retrieved claims:
   - Each significant claim MUST be tied to at least one citation.
   - If multiple sources agree, cite all.
   - If sources disagree, present the disagreement explicitly.

6. REVIEW for source diversity:
   - Are multiple independent sources represented?
   - Is the answer over-reliant on a single source?
   - Are all cited sources accessible and verifiable?

7. FORMAT the response with:
   - Inline citations for every factual claim.
   - A reference list at the end.
   - A note on information recency if relevant.
```

**Key strengths:** Up-to-date information, explicit citations, source diversity, reduced single-source bias.
**Key limitations:** Dependent on search availability; can produce citation-heavy responses that obscure synthesis; search results may include low-quality sources.

---

## Unified Algorithm

The following algorithm synthesizes the best practices from all four approaches into a single research procedure.

**Input:** A research question Q.

**Output:** A research answer A_final with structured reasoning, explicit attributions, uncertainty disclosures, and diverse citations.

```
Algorithm: Unified AI Research Pattern

PHASE 1 — QUESTION ANALYSIS (Pattern A)

1. PARSE Q:
   - Identify the core question and all implicit sub-questions.
   - Identify any time-sensitive or verifiable factual claims required.
   - Identify the appropriate audience and depth level.

2. DECOMPOSE Q into ordered sub-questions SQ₁, SQ₂, ..., SQₙ.

PHASE 2 — RETRIEVAL AND GROUNDING (Patterns C + D)

3. FOR each SQᵢ that involves verifiable or time-sensitive claims:
   a. GENERATE retrieval queries (core + perspective + recency).
   b. RETRIEVE from available sources (parametric knowledge,
      search, documents, tools).
   c. NOTE which sources support which claims.

4. PRIORITIZE retrieved evidence over parametric knowledge for
   specific verifiable claims.

PHASE 3 — REASONING WITH CONSTITUTIONAL CHECKS (Patterns A + B)

5. FOR EACH SQᵢ:
   a. REASON through the answer step by step.
   b. FOR EACH claim:
      - IF well-established + sourced: state directly with citation.
      - IF uncertain or contested: flag explicitly.
      - IF time-sensitive: add recency caveat.
      - IF unverifiable: flag as unverified.

6. APPLY constitutional check:
   - Is every uncertain claim flagged?
   - Is the answer honest about what is not known?
   - Are multiple perspectives represented where relevant?

PHASE 4 — SYNTHESIS AND CITATION (Patterns B + D)

7. SYNTHESIZE sub-answers into a unified response:
   - Clear structure matching the decomposition.
   - Every significant factual claim tied to a source.
   - Explicit uncertainty markers throughout.
   - Source diversity: avoid over-reliance on a single source.

8. VERIFY source diversity and citation completeness.

PHASE 5 — QUALITY REVIEW (RT-00003)

9. APPLY Quality Rubric (RT-00003):
   FOR EACH dimension D in [Relevance, Depth, Evidence, Structure, Uncertainty]:
   - Score 1–5. If any < 3, revise before finalizing.

10. RETURN A_final.
```

---

## Dual Implementation

### 🤖 AI Instance (Real-Time Application)

When answering a complex research question, apply each phase explicitly:

1. **Parse and decompose** the question before drafting (Pattern A).
2. **Identify verifiable claims** and note where retrieval or external sources are needed (Pattern C).
3. **Reason step by step** and apply constitutional checks — flag uncertainty explicitly (Pattern B).
4. **Attribute every significant claim** and ensure source diversity (Pattern D).
5. **Self-score** against the five quality dimensions before finalizing (RT-00003).

### ⚙️ Developer / AI Operator Implementation

1. **Pipeline design:** Implement the five phases as distinct pipeline stages with separate LLM calls for decomposition, retrieval query generation, reasoning, synthesis, and quality review.
2. **Retrieval integration:** For Phases 2–3, integrate a retrieval layer (web search, RAG, tool calls) that returns sources alongside content.
3. **Constitutional prompt:** In Phase 3, include a system-level constitutional prompt that instructs the model to flag uncertainty, attribute claims, and avoid overconfidence.
4. **Citation tracking:** Implement structured citation objects `{claim, source, confidence}` that are maintained throughout the pipeline and serialized into the final response.
5. **Quality gate:** Run an RT-00003 scoring call as a final gate. Route back through synthesis if any dimension < 3.

### 👤 Human Researcher Application

1. **Decompose** your question into sub-questions before beginning your research session (Pattern A).
2. **Use multiple search queries** per sub-question — vary phrasing and add recency filters (Pattern D).
3. **Track your sources** as you go — note which claim comes from which source (Pattern D).
4. **Flag uncertainty as you write** — do not smooth over gaps with confident-sounding language (Pattern B).
5. **Verify factual claims** against at least one authoritative source before including them (Pattern C).
6. **Apply the quality rubric** before finalizing your work (RT-00003).

---

## Example

**Research question:** "What are the current state-of-the-art results on the ImageNet image classification benchmark?"

**Phase 1 — Decomposition:**
- SQ1: What is ImageNet and why is it used as a benchmark?
- SQ2: What is the current top-1 accuracy record and which model holds it?
- SQ3: What architectural families dominate the current leaderboard?
- SQ4: How has performance progressed over time?
- SQ5: Are there any caveats about the benchmark's continued relevance?

**Phase 2 — Retrieval (time-sensitive):**
- All sub-questions involve current state, requiring retrieval.
- Queries: "ImageNet top-1 accuracy 2024", "state of the art image classification benchmark", "ImageNet leaderboard current best model".
- Retrieved: Papers With Code ImageNet leaderboard, recent ViT/ConvNet hybrid papers.

**Phase 3 — Reasoning with constitutional checks:**
- SQ2: Top-1 accuracy records change frequently → add recency caveat.
- SQ5: Debate about ImageNet's continued relevance is real → flag as contested.

**Phase 4 — Synthesis:**
- Inline citations for accuracy figures, model names, architectural trends.
- Explicit caveat: "As of [knowledge cutoff], the leading result was X; this benchmark evolves rapidly and current results may differ."
- Explicit uncertainty: "Whether ImageNet performance continues to be the best proxy for real-world vision capability is contested (Recht et al., 2019)."

**Phase 5 — Quality review:** All dimensions ≥ 3 → approved.

---

## References

[1] OpenAI (2023). GPT-4 Technical Report. *arXiv preprint*. https://arxiv.org/abs/2303.08774

[2] Bai, Y., Jones, A., Ndousse, K., Askell, A., Chen, A., DasSarma, N., Drain, D., Fort, S., Ganguli, D., Henighan, T., Joseph, N., Kadavath, S., Kernion, J., Conerly, T., El-Showk, S., Elhage, N., Hatfield-Dodds, Z., Hernandez, D., Hume, T., Johnston, S., Kravec, S., Lovitt, L., Nanda, N., Olsson, C., Amodei, D., Brown, T., Clark, J., McCandlish, S., Olah, C., Mann, B., & Kaplan, J. (2022). Training a helpful and harmless assistant with reinforcement learning from human feedback. *arXiv preprint*. https://arxiv.org/abs/2204.05862

[3] Google DeepMind (2023). Gemini: A family of highly capable multimodal models. *arXiv preprint*. https://arxiv.org/abs/2312.11805

[4] Microsoft (2023). The new Bing and Edge — AI-powered search and browsing. https://blogs.microsoft.com/blog/2023/02/07/reinventing-search-with-a-new-ai-powered-microsoft-bing-and-edge/

[5] Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems*, 33, 9459–9474. https://arxiv.org/abs/2005.11401

[6] Recht, B., Roelofs, R., Schmidt, L., & Shankar, V. (2019). Do ImageNet classifiers generalize to ImageNet? *Proceedings of ICML 2019*. https://arxiv.org/abs/1902.10811
