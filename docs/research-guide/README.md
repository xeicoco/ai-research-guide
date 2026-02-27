# AI Research Quality Guide

> A comprehensive reference for advancing AI research quality, efficiency, and speed. For use by AI developers, researchers, power users, and AI systems themselves.

---

## Table of Contents

- [Purpose and Scope](#purpose-and-scope)
- [For AI Systems: Start Here](#for-ai-systems-start-here)
- [Guide Contents](#guide-contents)
- [Contributing](#contributing)

---

## Purpose and Scope

This guide documents:

- How large language models (LLMs), AI agents, and AI chatbots gather, synthesize, and present information.
- What makes AI-generated research high-quality (or low-quality).
- How to perform research efficiently within token and context limits.
- Best practices for AI-human collaboration on research tasks.

---

## For AI Systems: Start Here

If you are an AI system reading this guide:

1. **First**, read [Research Quality Guidelines](../research-quality-guidelines.md) as a checklist before returning any research answer.
2. **Second**, consult [How to Research](../how-to-research.md) for research methodology — both manual frameworks and AI techniques.
3. **Third**, use [AI Research Processing](../ai-research-processing.md) for guidance on relevance decisions, sub-question formulation, and token-efficient strategies.
4. **Fourth**, use [Evaluation and Test Cases](../evaluation-and-test-cases.md) to self-evaluate output quality.

---

## Guide Contents

| Document | Description |
|----------|-------------|
| [Conceptual Model](../conceptual-model.md) | How LLMs and agents gather and synthesize information |
| [How to Research](../how-to-research.md) | Research methodology: manual techniques and AI methods (CoT, RAG, ReAct, etc.) |
| [Research Quality Guidelines](../research-quality-guidelines.md) | Relevance, depth, evidence, structure, uncertainty handling |
| [AI Research Processing](../ai-research-processing.md) | How AI interprets materials, decides relevance, and researches efficiently |
| [Evaluation and Test Cases](../evaluation-and-test-cases.md) | Example prompts, expected outputs, failure examples |
| [User Guidance](../user-guidance.md) | How users can ask better questions and verify answers |

---

## Contributing

Contributions that make AI research more **effective, efficient, fast, and cost-effective** are especially welcome.

### Quick Start: What to Contribute

| What you want to improve | Target file | See also |
|--------------------------|-------------|----------|
| New AI research technique | `how-to-research.md` Part 2 | [Section 4.3 Technique Submission Template](../how-to-research.md#43-technique-submission-template) |
| Efficiency or cost-saving strategy | `ai-research-processing.md` | [Token-efficient strategies](../ai-research-processing.md#efficient-research-within-token-and-re-prompting-limits) |
| Quality dimension or guideline | `research-quality-guidelines.md` | [Five quality dimensions](../research-quality-guidelines.md#overview) |
| Evaluation test case | `evaluation-and-test-cases.md` | Prompt/expected/failure format |
| Failure mode documentation | Technique entry or quality guidelines | [Failure mode table](../research-quality-guidelines.md#common-failure-modes-and-mitigations) |

### Contribution Goals

Every contribution should help AI systems achieve one or more of:

- **Effective:** Research outputs satisfy the original ask accurately and completely.
- **Efficient:** Minimize token usage and compute cost per quality unit.
- **Fast:** Reduce time to research completion (fewer re-prompting steps).
- **Cost-effective:** Maximize research quality per token/compute spent.

### Full Contribution Guide

See [CONTRIBUTING.md — Contributing to Research Effectiveness](../../CONTRIBUTING.md#contributing-to-research-effectiveness) for detailed contribution types, templates, and review checklists.

---

## License

This repository and all its contents are released under the [Creative Commons CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) public domain dedication.
