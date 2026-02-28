# RT-00004: User Query Facilitation

> **Part of the [Research Techniques Catalog](README.md)**

**Technique name:** User Query Facilitation

**Purpose:** Enable an AI mediator/persona to bridge between a human user and AI research agents — improving user queries, facilitating research with downstream agents, and presenting results back to users in an accessible and trustworthy form.

---

## Description and Rationale

User Query Facilitation formalizes the strategies from human user guidance (asking specifically, providing context, requesting structure, acknowledging uncertainty) into an algorithmic role for an AI intermediary agent. Rather than having the human user bear full responsibility for query quality, an AI facilitator absorbs that responsibility: it receives a raw user query, improves it, dispatches it to one or more research AI agents, evaluates the returned answer, and presents a vetted result to the user with appropriate caveats.

**Why this technique works:** End users often lack the expertise to formulate precise research queries, recognize low-quality AI outputs, or know when to distrust an answer. An AI facilitator applies systematic query enrichment and answer evaluation invisibly, raising the floor of answer quality across all users regardless of their prompt-engineering skill.

**Applicable to:** Conversational AI products with a mediator/orchestrator layer, multi-agent research pipelines, AI assistants with a user-facing front-end and a research back-end, and human facilitators managing AI-assisted research sessions.

---

## Evaluation Criteria Reference

This technique strengthens all five quality dimensions by operating at both the input (query) and output (answer) stages:

| Dimension | How User Query Facilitation Helps |
|-----------|-----------------------------------|
| **Relevance** | Query enrichment step forces disambiguation; facilitator verifies the answer addresses the enriched question |
| **Depth** | Facilitator explicitly requests structure and depth in the forwarded query |
| **Evidence** | Facilitator instructs research agents to cite sources; verifies citations before presenting to user |
| **Structure** | Facilitator requests explicit answer structure and reformats if needed |
| **Uncertainty** | Facilitator instructs agents to flag uncertainty; surfaces knowledge-cutoff and hedging to the user |

---

## Algorithm

**Input:** A raw user query Q_raw from a human user.

**Output:** A presented answer P with user-appropriate framing, caveats, and follow-up prompts.

```
Algorithm: User Query Facilitation

PHASE 1 — QUERY INTAKE AND ENRICHMENT

1. RECEIVE Q_raw from the user.

2. ASSESS query specificity:
   a. IF Q_raw is vague (no domain, no scope, no constraints):
      - IDENTIFY the most likely intended question.
      - GENERATE an enriched query Q_enriched with:
        * Specific scope (domain, time period, audience level)
        * Explicit depth requirement ("explain the mechanism, not just the outcome")
        * Structural request ("provide pros/cons", "step-by-step", "key points then detail")
        * Uncertainty flag instruction ("flag any claim you are not certain about")
   b. IF Q_raw is already specific:
      - CONFIRM scope is achievable; trim or split if too broad.
      - ADD uncertainty flag instruction if absent.

3. ASSESS context completeness:
   a. IF user context is missing (expertise level, purpose, constraints):
      - INFER likely context from Q_raw (e.g., domain keywords → expertise level).
      - EMBED inferred context into Q_enriched.
   b. IF context is present: preserve it verbatim in Q_enriched.

4. DECOMPOSE Q_enriched into sub-questions SQ = {SQ₁, SQ₂, ..., SQₙ}
   such that answering all SQᵢ fully answers Q_enriched.
   (Apply RT-00002 Self-Asking decomposition here.)

PHASE 2 — RESEARCH AGENT DISPATCH

5. FOR EACH SQᵢ in SQ:
   a. DISPATCH SQᵢ to one or more research AI agents.
   b. RECEIVE draft answer Aᵢ from each agent.

6. AGGREGATE all Aᵢ into a combined draft answer A_draft.

PHASE 3 — ANSWER EVALUATION

7. EVALUATE A_draft using RT-00001 (Chain-of-Thought Self-Evaluation):
   FOR EACH dimension D in [Relevance, Depth, Evidence, Structure, Uncertainty]:
   a. SCORE A_draft on D (1–5).
   b. IF score < 3: FLAG for revision.

8. VERIFY citations:
   a. FOR EACH citation C in A_draft:
      - CHECK that C is internally consistent (author, title, year, venue match).
      - FLAG any citation that cannot be verified as potentially fabricated.
   b. ANNOTATE flagged citations with a warning before presenting to user.

9. ASSESS knowledge-cutoff risk:
   a. IF Q_enriched involves time-sensitive information (events, regulations, prices,
      current state of science):
      - ADD a recency caveat to the answer.

10. IF any dimension scored < 3 in step 7:
    a. IDENTIFY specific passages to revise.
    b. RE-QUERY the research agents with targeted follow-up questions.
    c. INTEGRATE improved content.
    d. RE-EVALUATE until all dimensions ≥ 3.

PHASE 4 — USER PRESENTATION

11. FORMAT the final answer A_final for the user:
    a. OPEN with a one-sentence restatement of the question as understood
       (allows user to catch misinterpretation).
    b. PRESENT the answer with clear structure matching the user's stated or
       inferred needs (structured overview, step-by-step, pros/cons, etc.).
    c. SURFACE all uncertainty flags as visible caveats (not buried in body text).
    d. ANNOTATE any citation warnings from step 8.
    e. ADD a recency caveat if triggered in step 9.

12. OFFER follow-up scaffolding:
    a. LIST 2–3 sub-questions the user might want to explore next.
    b. SUGGEST authoritative external sources for any medical, legal, financial,
       or safety-critical aspects of the answer.
    c. IF the answer has low overall confidence: RECOMMEND the user verify with
       a domain expert or primary source.

13. RETURN P (the presented answer with framing, caveats, and follow-up prompts).
```

---

## Dual Implementation

### 🤖 AI Instance (Real-Time Application)

When acting as a user-facing AI mediator, apply this technique on every incoming user query:

1. **Before dispatching to research agents:** restate the question internally as you understand it, enrich it with scope and depth requirements, and decompose into sub-questions.
2. **When receiving research output:** verify that each sub-question is answered; check citations for internal consistency; flag time-sensitive topics.
3. **Before presenting to the user:** open with a restatement, surface all uncertainty, and annotate any citation concerns explicitly.

**Example internal facilitator check:**
```
User asked: "What's the deal with CRISPR?"

→ Enriched query: "Explain the mechanism of CRISPR-Cas9 gene editing,
  its main agricultural and medical applications, key risks and ethical
  concerns, and current regulatory status. Flag any claims that are
  contested or may have changed since your training cutoff. Target:
  general educated audience."

→ Sub-questions: mechanism, applications (agriculture + medicine),
  risks, ethics, regulatory status, uncertainty/recency

→ After receiving research output:
  - Does it answer all 5 sub-questions? Check.
  - Are there specific citations? Verify internal consistency.
  - Is regulatory status time-sensitive? Yes → add recency caveat.
  - Open user response with: "I understood you to be asking about
    how CRISPR works and its current uses and risks — here's what I found:"
```

### ⚙️ Developer / AI Operator Implementation

Implement User Query Facilitation as a multi-stage orchestration pipeline:

1. **Query enrichment stage:** Run a dedicated enrichment call with a system prompt that includes the query specificity and context rules from Phase 1. Output a structured `enriched_query` object with fields: `core_question`, `scope`, `audience_level`, `depth_requirement`, `structural_format`, `uncertainty_instruction`.

2. **Sub-question decomposition:** Apply RT-00002 decomposition to produce `sub_questions[]`. Use these as individual retrieval queries for RAG pipelines to improve recall.

3. **Multi-agent dispatch:** Route each sub-question to the appropriate research agent (general LLM, web search, specialized domain tool). Aggregate results.

4. **Evaluation gate:** Apply RT-00001 CoT scoring as an automated post-generation step. Implement a routing rule: if `min(scores) < 3`, re-query with the critique appended to context (maximum 2 retry iterations).

5. **Citation verification:** Integrate a citation consistency checker (CrossRef API, DOI lookup, or a dedicated verification LLM call) to flag potentially fabricated references before user presentation.

6. **Presentation templating:** Use a structured output template that enforces: question restatement → answer body → uncertainty caveats → citation warnings → follow-up suggestions.

### 👤 Human Facilitator Application

For a human facilitator mediating between a user and an AI research tool:

1. **Receive the user's question** and ask yourself: *Is this specific enough to get a useful answer?* If not, rephrase it before submitting to the AI.
2. **Add context** the user may not have thought to include: their purpose, their level of expertise, and any constraints (length, format, jargon).
3. **Break complex questions** into focused sub-questions and submit them separately.
4. **When reading the AI's answer:** apply the evaluation checklist — does it answer the question? Are claims specific and concrete? Is uncertainty acknowledged? Could it be outdated?
5. **Verify citations** independently before passing them to the user.
6. **Present the answer to the user** with clear framing: restate the question as you understood it, highlight any uncertainty, flag any unverified citations, and recommend authoritative sources for high-stakes topics (medical, legal, financial, safety).

---

## Example

**Raw user query:** "Tell me about AI risks."

**Phase 1 — Enrichment:**

> *Enriched query:* "Provide a structured overview of the main categories of AI risk — technical (e.g., misalignment, hallucination), societal (e.g., bias, misuse, labor displacement), and governance-related (e.g., regulatory gaps). For each category, briefly explain the risk mechanism and give at least one documented example. Acknowledge any areas of active debate. Target: policy-literate non-technical audience. Flag any claims that are contested or may be outdated."

**Sub-questions decomposed:**
1. What are technical AI risks and their mechanisms?
2. What are societal AI risks and documented examples?
3. What are governance/regulatory AI risks?
4. Which of these risks are contested vs. well-established?
5. What is the current regulatory landscape (knowledge cutoff caveat)?

**Phase 3 — Evaluation (abbreviated):**
- Relevance: 5 — enriched query directly scopes the answer
- Depth: 4 — mechanisms and examples present; some quantification missing
- Evidence: 3 — claims hedged but few specific citations → flag for user
- Structure: 5 — organized by risk category
- Uncertainty: 4 — knowledge cutoff noted; active debates flagged

**Phase 4 — Presented to user:**
> "I understood your question as asking for an overview of AI risks by category (technical, societal, governance). Here is what the current literature says: [structured answer]. **Note:** The regulatory landscape is changing rapidly; information here reflects the state as of the AI's knowledge cutoff. **Citation note:** Some claims in this answer lack specific citations — I recommend verifying key claims with primary sources such as the EU AI Act text or peer-reviewed AI safety surveys. You might also want to explore: (1) technical AI safety in more depth, (2) bias and fairness in AI systems, or (3) the EU AI Act specifically."

---

## References

- Meriam Library, California State University, Chico. (2010). *Evaluating Information — Applying the CRAAP Test*. https://library.csuchico.edu/help/source-or-information-good-use-craap-test
- Caulfield, M. (2019). *SIFT (The Four Moves)*. Hapgood. https://hapgood.us/2019/06/19/sift-the-four-moves/
- Ji, Z., Lee, N., Frieske, R., Yu, T., Su, D., Xu, Y., Ishii, E., Bang, Y. J., Madotto, A., & Fung, P. (2023). Survey of hallucination in natural language generation. *ACM Computing Surveys*, 55(12), 1–38. https://doi.org/10.1145/3571730
- Guo, Z., Schlichtkrull, M., & Vlachos, A. (2022). A survey on automated fact-checking. *Transactions of the Association for Computational Linguistics*, 10, 178–206. https://doi.org/10.1162/tacl_a_00454
- Bommasani, R., et al. (2021). On the opportunities and risks of foundation models. *arXiv preprint*. https://arxiv.org/abs/2108.07258
- Press, O., et al. (2022). "Measuring and Narrowing the Compositionality Gap in Language Models." *EMNLP 2023.*
- Wei, J., et al. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models." *NeurIPS 2022.*

See also: [RT-00001 Chain-of-Thought Self-Evaluation](RT-00001-chain-of-thought-self-evaluation.md), [RT-00002 Self-Asking Evaluation](RT-00002-self-asking-evaluation.md), [User Guidance](../user-guidance.md).
