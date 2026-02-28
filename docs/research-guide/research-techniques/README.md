# Research Techniques Catalog

> **Part of the [AI Research Quality Guide](../README.md)**

A community-extensible catalog of algorithmic research techniques for AI research quality. Each technique provides a formal algorithm, theoretical rationale, and dual implementation guidance for AI systems and developers/humans.

---

## Table of Contents

- [Purpose](#purpose)
- [How to Use This Catalog](#how-to-use-this-catalog)
- [Evaluation Criteria Reference](#evaluation-criteria-reference)
- [Technique Index](#technique-index)
- [Contributing New Techniques](#contributing-new-techniques)

---

## Purpose

This catalog replaces a static collection of test cases with an algorithmic, extensible set of research techniques. Each technique:

- Provides a **formal algorithm** that AI systems can apply in real-time
- Provides a **dual implementation** guide for AI instances and developers/operators
- Is **community-contributed** — anyone can add new techniques
- Can be applied **independently or in combination** for comprehensive evaluation

---

## How to Use This Catalog

| Audience | Recommended usage |
|----------|-------------------|
| **AI systems** | Apply techniques as self-evaluation steps before returning research answers |
| **Developers/operators** | Implement techniques as post-generation validation pipeline steps |
| **Evaluators/reviewers** | Use techniques as structured rubrics for peer review and benchmarking |
| **Contributors** | Add new technique files following the [standard format](#contributing-new-techniques) |

Techniques can be applied individually or in combination. For comprehensive evaluation:

1. Start with [RT-00002 Self-Asking](RT-00002-self-asking-evaluation.md) to verify completeness
2. Apply [RT-00001 Chain-of-Thought](RT-00001-chain-of-thought-self-evaluation.md) to reason through quality
3. Finalize with [RT-00003 Quality Rubric](RT-00003-quality-rubric-application.md) for a scored assessment

---

## Evaluation Criteria Reference

All techniques operate over the five quality dimensions defined in [`research-quality-guidelines.md`](../research-quality-guidelines.md):

| Dimension | Key Question | Score 1 (Poor) | Score 5 (Excellent) |
|-----------|-------------|----------------|---------------------|
| **Relevance** | Does the answer directly address the question? | Off-topic or misses the question | Directly and completely addresses the question |
| **Depth** | Is the level of detail appropriate and sufficient? | Surface-level or too vague | Thorough, with nuance and detail |
| **Evidence** | Are claims supported or appropriately hedged? | No sources; claims unsupported | All major claims sourced or hedged |
| **Structure** | Is the answer clear, well-organized, and scoped? | Hard to follow | Clear, well-organized, appropriate length |
| **Uncertainty** | Are uncertain or contested claims flagged? | No hedging on uncertain claims | Accurate uncertainty representation throughout |

---

## Technique Index

| ID | Technique | Focus | Best for |
|----|-----------|-------|---------|
| [RT-00001](RT-00001-chain-of-thought-self-evaluation.md) | Chain-of-Thought Self-Evaluation | Step-by-step dimension reasoning | General-purpose pre-output self-check |
| [RT-00002](RT-00002-self-asking-evaluation.md) | Self-Asking Evaluation | Sub-question decomposition and coverage | Complex multi-part questions |
| [RT-00003](RT-00003-quality-rubric-application.md) | Quality Rubric Application | Structured scoring with justification | Formal evaluation, benchmarking, peer review |
| [RT-00004](RT-00004-user-query-facilitation.md) | User Query Facilitation | Query enrichment, agent dispatch, answer vetting, user presentation | AI mediator/orchestrator bridging users and research agents |
| [RT-00005](RT-00005-iterative-research-questioning.md) | Iterative Research Questioning | Systematic knowledge-gap identification and next-question formulation | Progressive research workflows requiring iterative depth |
| [RT-00006](RT-00006-ai-chatbot-research-patterns.md) | AI Chatbot Research Patterns | Survey and unification of leading AI chatbot research approaches | Learning from ChatGPT, Claude, Gemini, and Copilot patterns |

*Future techniques: CoT-with-retrieval verification, Socratic questioning, adversarial self-critique, multi-perspective synthesis check — [contribute yours](#contributing-new-techniques).*

---

## Contributing New Techniques

New research techniques are welcome from the community. A technique qualifies for inclusion when it:

1. Provides a **formal, reproducible algorithm** that can be followed step-by-step
2. Is applicable in **real-time by an AI system** and/or implementable by a developer
3. Addresses at least one of the five quality dimensions
4. Includes at least one **worked example**
5. Includes **references** to supporting academic work (where available)

### File naming convention

```
RT-NNNNN-short-technique-name.md
```
where `NNNNN` is the next available 5-digit number (e.g., `RT-00007`).

### Standard technique file structure

```markdown
# RT-NNNNN: [Technique Name]

> **Part of the [Research Techniques Catalog](README.md)**

**Technique name:** [Full name]
**Purpose:** [One sentence]

---

## Description and Rationale
[What it is, why it works, who it's applicable to]

## Evaluation Criteria Reference
[Which dimensions it strengthens and how]

## Algorithm
[Formal numbered algorithm with Input/Output specification]

## Dual Implementation
### 🤖 AI Instance (Real-Time Application)
### ⚙️ Developer / AI Operator Implementation
### 👤 Human Researcher / Reviewer Application

## Example
[Worked example showing the technique in action]

## References
[Academic citations]
```

See existing technique files for examples of this format in practice.

To contribute: open a pull request following [contributor-guide.md](../contributor-guide.md).
