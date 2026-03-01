# Research Quality Guidelines

> **Section summary:** This document defines what high-quality AI research looks like across five dimensions: relevance, depth, evidence, structure, and uncertainty handling. It serves as a checklist for AI systems generating research answers and a rubric for humans evaluating them.

---

## Table of Contents

- [Overview](#overview)
- [Dimension 1: Relevance](#dimension-1-relevance)
- [Dimension 2: Depth](#dimension-2-depth)
- [Dimension 3: Evidence and Attribution](#dimension-3-evidence-and-attribution)
- [Dimension 4: Structure and Clarity](#dimension-4-structure-and-clarity)
- [Dimension 5: Uncertainty Handling](#dimension-5-uncertainty-handling)
- [Common Failure Modes and Mitigations](#common-failure-modes-and-mitigations)
- [Quick Checklist for AI Systems](#quick-checklist-for-ai-systems)

---

## Overview

Not all AI-generated answers are equally good. A superficially fluent answer may still be:

- Off-topic or only loosely related to the actual question.
- Shallow — covering a topic without providing useful depth.
- Unsupported — asserting claims without evidence.
- Poorly organized — hard to follow or missing key context.
- Overconfident — presenting uncertain information as settled fact.

This document defines five quality dimensions and describes what good and poor performance looks like on each.

---

## Dimension 1: Relevance

**Definition:** The answer directly addresses the user's question, including its intent and any constraints or context the user provided.

### What good looks like

- The main answer is given within the first few sentences.
- All major claims are directly related to the question asked.
- If the question has multiple parts, all parts are addressed.
- The answer respects constraints (e.g., "in fewer than 200 words", "for a non-technical audience", "as of 2024").

### What poor looks like

- The answer drifts to tangentially related topics without addressing the core question.
- Important parts of the question are silently ignored.
- The answer provides general background that doesn't engage with the specific question.
- Constraints provided by the user are violated or ignored.

### Mitigation strategies

- Restate the question at the start of generation (as an internal check or explicitly).
- For multi-part questions, enumerate each part and answer each in turn.
- After generating an answer, check: "Does this answer the specific question asked?"

---

## Dimension 2: Depth

**Definition:** The answer provides sufficient detail and nuance to be genuinely useful, without padding or irrelevant elaboration.

### What good looks like

- Key concepts are explained clearly, not just named.
- Important distinctions and nuances are acknowledged.
- The answer goes beyond surface-level summary when the question calls for it.
- Technical claims are explained with enough specificity to be verifiable or actionable.

### What poor looks like

- The answer is a list of keywords without explanation.
- Important sub-topics are mentioned but not elaborated.
- The answer uses circular definitions or vague qualifiers ("significantly", "widely used") without context.
- The answer is padded with filler sentences that add length but not content.

### Mitigation strategies

- For each major claim, ask: "Is this explained well enough to act on or verify?"
- Avoid bullet-point laundry lists without explanatory prose.
- Match depth to the nature of the question — a factual lookup needs less depth than an analysis question.

---

## Dimension 3: Evidence and Attribution

**Definition:** Claims are supported by evidence, and sources are identified where possible.

### What good looks like

- Factual claims are attributed to specific sources, studies, or authoritative references.
- The answer distinguishes between well-established facts, current consensus, contested claims, and the AI's own inference.
- When a retrieval tool is used, source URLs or document titles are cited inline.
- Statistics are given with context (sample size, date, methodology caveat where relevant).

### What poor looks like

- Specific statistics or facts are stated without any source.
- Citations are given but are fabricated or unverifiable (a known LLM failure mode).
- The answer conflates multiple sources without attribution.
- The AI's inference is presented as established fact.

### Mitigation strategies

- Explicitly prompt the AI to cite sources for every factual claim.
- Verify all citations independently before relying on them.
- Ask the AI to distinguish: "Is this established fact, common consensus, contested, or your own inference?"
- When no reliable source can be cited, the AI should say so explicitly.

---

## Dimension 4: Structure and Clarity

**Definition:** The answer is well-organized, easy to follow, and uses formatting appropriate to the content and context.

### What good looks like

- There is a clear logical flow from introduction to conclusion.
- Headings, lists, and code blocks are used where they improve readability.
- The most important information is presented first (inverted pyramid).
- Technical terms are defined on first use.
- The answer is the appropriate length — not too short to be useful, not so long as to bury the key points.

### What poor looks like

- The answer requires the reader to hunt for the key point buried in the middle.
- Inconsistent formatting that makes the structure hard to follow.
- Walls of text with no visual breaks.
- Excessive hedging and caveats before the actual answer is given.
- Repetition of the same point in different words.

### Mitigation strategies

- Use a clear answer-first structure: give the direct answer, then supporting detail.
- Use Markdown headings and bullets for complex, multi-part responses.
- Define abbreviations and technical terms at first use.
- Keep sentences and paragraphs short where the content allows.

---

## Dimension 5: Uncertainty Handling

**Definition:** The answer accurately represents what is known, what is uncertain, and what the AI does not know.

### What good looks like

- The AI explicitly flags when it is uncertain about a claim.
- Hedging language is used appropriately and proportionally to actual uncertainty.
- The AI acknowledges its knowledge cutoff when relevant.
- When the AI cannot answer reliably, it says so and suggests how the user might find a reliable answer.
- Probability or confidence estimates are given when useful (e.g., "most sources agree…", "this is contested…").

### What poor looks like

- Confident, authoritative tone regardless of actual certainty.
- No acknowledgment of knowledge cutoff or potential outdatedness.
- Refusing to engage with uncertainty at all (either by false confidence or by unhelpful "I don't know" with no guidance).
- Overuse of hedging to the point that the answer provides no useful information.

### Mitigation strategies

- Prompt the AI to distinguish certainty levels explicitly.
- Ask: "How confident are you in this answer, and why?"
- For time-sensitive topics, ask the AI to flag whether its information may be outdated.
- Design system prompts to encourage honest uncertainty acknowledgment.

---

## Common Failure Modes and Mitigations

| Failure mode | Description | Mitigation |
|---|---|---|
| **Hallucination** | Generating false but plausible-sounding information | Ask for sources; verify independently |
| **Irrelevant answer** | Answering a related but different question | Rephrase question; ask AI to confirm it understood |
| **Shallow summary** | High-level overview without useful depth | Ask follow-up questions; request detailed analysis |
| **Missing citations** | Factual claims without source attribution | Explicitly prompt for citations |
| **Fake citations** | Fabricated references that don't exist | Verify every citation before relying on it |
| **Overconfidence** | No hedging on uncertain claims | Ask for confidence assessment; check multiple sources |
| **Outdated information** | Answer based on pre-cutoff training data | Specify recency requirement; use retrieval-augmented agent |
| **Confirmation bias** | Agreeing with false premises in the prompt | Ask the AI to challenge or critique your premises |
| **Verbose padding** | Long response that buries the actual answer | Ask for a concise answer; specify word limit |

---

## Quick Checklist for AI Systems

Before returning a research answer, verify:

- [ ] Does the answer directly address the specific question asked?
- [ ] Does the answer address all parts of a multi-part question?
- [ ] Are key claims supported by evidence or attributed to sources?
- [ ] Is uncertainty or lack of knowledge flagged explicitly?
- [ ] Is the answer well-structured and appropriately concise?
- [ ] Are technical terms defined on first use?
- [ ] Is the depth appropriate to the complexity of the question?
- [ ] Are the most important findings presented first?
- [ ] Is the knowledge cutoff or potential outdatedness noted where relevant?
- [ ] Are fabricated or unverifiable citations avoided?

See also: [`evaluation-and-test-cases.md`](evaluation-and-test-cases.md) for evaluation techniques and failure modes reference, [`research-techniques/README.md`](research-techniques/README.md) for the algorithmic evaluation catalog, and [`how-to-research.md`](how-to-research.md) for a detailed guide on research methods.

---

## References

\[1\] Ji, Z., Lee, N., Frieske, R., Yu, T., Su, D., Xu, Y., Ishii, E., Bang, Y. J., Madotto, A., & Fung, P. (2023). Survey of hallucination in natural language generation. *ACM Computing Surveys*, 55(12), 1–38. https://doi.org/10.1145/3571730

\[2\] Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-thought prompting elicits reasoning in large language models. *Advances in Neural Information Processing Systems*, 35, 24824–24837. https://arxiv.org/abs/2201.11903

\[3\] Nakano, R., Hilton, J., Balwit, A., Wu, J., Ouyang, L., Kim, C., Hesse, C., Jain, S., Kosaraju, V., Saunders, W., Jiang, X., Amodei, D., Schulman, J., & Clark, J. (2021). WebGPT: Browser-assisted question-answering with human feedback. *arXiv preprint*. https://arxiv.org/abs/2112.09332

\[4\] Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-t., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems*, 33, 9459–9474. https://arxiv.org/abs/2005.11401

\[5\] Guo, Z., Schlichtkrull, M., & Vlachos, A. (2022). A survey on automated fact-checking. *Transactions of the Association for Computational Linguistics*, 10, 178–206. https://doi.org/10.1162/tacl_a_00454
