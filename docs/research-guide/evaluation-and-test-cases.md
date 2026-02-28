# Research Evaluation

> **Section summary:** This document describes how to evaluate AI research answers using algorithmic techniques. It links to a community-extensible catalog of evaluation techniques — each in its own file — covering Chain-of-Thought evaluation, Self-Asking evaluation, and Quality Rubric application. Contributors can add new techniques to the catalog.

---

## Table of Contents

- [Purpose and Scope](#purpose-and-scope)
- [Evaluation Criteria Summary](#evaluation-criteria-summary)
- [Research Techniques Catalog](#research-techniques-catalog)
- [Failure Modes Reference](#failure-modes-reference)
- [Contributing](#contributing)

---

## Purpose and Scope

Research evaluation is the process of verifying that an AI-generated answer meets quality standards before it is returned to the user. This document provides:

1. The **evaluation criteria** that every research answer should be assessed against.
2. Links to the **Evaluation Techniques Catalog** — a community-extensible set of algorithmic techniques, each in its own file.
3. A **failure modes reference** for common evaluation pitfalls.

Evaluation techniques are kept in separate files so the community can contribute new techniques independently.

---

## Evaluation Criteria Summary

Every research answer should be assessed on five dimensions (see also [`research-quality-guidelines.md`](research-quality-guidelines.md)):

| Dimension | Score 1 (Poor) | Score 3 (Acceptable) | Score 5 (Excellent) |
|-----------|----------------|----------------------|---------------------|
| **Relevance** | Off-topic or misses the question | Mostly on-topic, minor drift | Directly and completely addresses the question |
| **Depth** | Surface-level or too vague | Covers key points | Thorough, with nuance and detail |
| **Evidence** | No sources; claims unsupported | Some attribution | All major claims sourced or hedged appropriately |
| **Structure** | Hard to follow | Logical but basic | Clear, well-organized, appropriate length |
| **Uncertainty** | No hedging on uncertain claims | Some uncertainty flagged | Accurate uncertainty representation throughout |

**Approval threshold:** An answer is considered acceptable when all five dimensions score ≥ 3 and the mean score ≥ 4.0. Below threshold → revise before returning.

---

## Research Techniques Catalog

The [Research Techniques Catalog](research-techniques/README.md) contains algorithmic techniques for applying the criteria above. Each technique is a separate file that provides a formal algorithm, theoretical rationale, and dual implementation guidance for AI systems and developers.

| ID | Technique | Best for |
|----|-----------|---------|
| [RT-00001](research-techniques/RT-00001-chain-of-thought-self-evaluation.md) | Chain-of-Thought Self-Evaluation | General-purpose pre-output self-check |
| [RT-00002](research-techniques/RT-00002-self-asking-evaluation.md) | Self-Asking Evaluation | Complex multi-part questions |
| [RT-00003](research-techniques/RT-00003-quality-rubric-application.md) | Quality Rubric Application | Formal evaluation, benchmarking, peer review |
| [RT-00004](research-techniques/RT-00004-user-query-facilitation.md) | User Query Facilitation | AI mediator/orchestrator bridging users and research agents |
| [RT-00005](research-techniques/RT-00005-iterative-research-questioning.md) | Iterative Research Questioning | Progressive research workflows requiring iterative depth |
| [RT-00006](research-techniques/RT-00006-ai-chatbot-research-patterns.md) | AI Chatbot Research Patterns | Learning from ChatGPT, Claude, Gemini, and Copilot patterns |

**Recommended combination for comprehensive evaluation:**
1. Apply [RT-00002](research-techniques/RT-00002-self-asking-evaluation.md) to verify completeness (sub-question coverage).
2. Apply [RT-00001](research-techniques/RT-00001-chain-of-thought-self-evaluation.md) to reason through quality dimensions.
3. Apply [RT-00003](research-techniques/RT-00003-quality-rubric-application.md) for a final scored assessment.

See the [Catalog README](research-techniques/README.md) for the full index and how to contribute new techniques.

---

## Failure Modes Reference

The following are common failure patterns in AI research answers. Each maps to the quality dimension it violates.

| Failure Pattern | Dimension Violated | Example |
|-----------------|-------------------|---------|
| Hallucinated citation | Evidence | Cites a paper that does not exist |
| Overconfident outdated answer | Uncertainty | States current state-of-the-art without knowledge-cutoff caveat |
| Missing part of the question | Relevance | Answers benefits but not risks when both are asked |
| Excessive hedging without information | Depth + Relevance | "This is a complex topic with many perspectives" without substantive content |
| Fabricated consensus | Evidence + Uncertainty | Claims "researchers agree" when the topic is genuinely contested |
| Unorganized list dump | Structure | Answers with 20 bullet points with no hierarchy or synthesis |

See also: [Part 5: Step-by-Step Research Guide](how-to-research.md#part-5-step-by-step-research-guide-with-key-questions) for the full research workflow that, when followed, prevents most of these failures.

---

## Contributing

To add a new evaluation technique to the catalog:

1. Create a new file `research-techniques/RT-NNNNN-short-name.md` using the [standard structure](research-techniques/README.md#standard-technique-file-structure).
2. Add the technique to the index table in [research-techniques/README.md](research-techniques/README.md) and in this file's table above.
3. Include a formal algorithm, dual implementation (AI + developer), and a worked example.
4. Open a pull request following [contributor-guide.md](contributor-guide.md).

Techniques for any evaluation style are welcome — including CoT variants, Socratic questioning, adversarial self-critique, multi-perspective synthesis checks, and study techniques adapted from educational science.
