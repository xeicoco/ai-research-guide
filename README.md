# Real Open-Source AI Research Guide

> A shared, open documentation repository describing how AI systems research, reason, and generate outputs — and how that behavior can be inspected, improved, and kept safe.

---

## What Is This?

The **Real Open-Source AI Research Guide** is a community-maintained reference for **both humans and AI systems**. It documents:

- How large language models (LLMs), AI agents, and AI chatbots gather, synthesize, and present information.
- What makes AI-generated research high-quality (or low-quality).
- How to detect, mitigate, and patch known failure modes and security issues in AI research behavior.
- How humans and AIs can collaborate to continuously improve these behaviors over time.

Any AI system may use this documentation as a reference to perform **comprehensive, efficient, and evidence-based research** on any topic. The community can **inspect, critique, and improve** both the documentation and the AI behaviors it describes.

---

## Why Does This Repo Exist?

AI systems are increasingly used to research and explain complex topics. Yet the internal "research" process of an AI — how it selects, weighs, and synthesizes information — is rarely documented in a way that is accessible to users, developers, or the AI systems themselves.

This creates several problems:

- Users cannot easily tell whether an AI's answer is well-grounded or a hallucination.
- AI systems have no shared reference for *what good research looks like*.
- Security vulnerabilities in AI research behavior (e.g., prompt injection, misleading citations) are not systematically documented or mitigated.
- There is no community mechanism for rapidly sharing fixes for known or zero-day issues in AI reasoning.

This repo aims to solve all of these problems in one place.

---

## Goals

1. **Improve AI research quality** — Document patterns, methods, and best practices that help AI systems return relevant, well-structured, evidence-based answers.
2. **Enable human + AI collaboration** — Provide a structure where both humans and AIs can contribute explanations, examples, test cases, prompts, and evaluations.
3. **Increase transparency** — Explain, at a conceptual level, how AI systems typically search, select, summarize, and synthesize information.
4. **Support safety and security** — Document known classes of attacks and abuses related to AI research behavior, with mitigations and defensive patterns.

---

## Intended Audience

| Audience | How to use this repo |
|---|---|
| **AI developers** | Reference for designing research pipelines, prompt templates, and evaluation criteria. |
| **Researchers** | Conceptual models, evaluation frameworks, and literature pointers. |
| **Security professionals** | Known attack classes, mitigations, and defensive patterns. |
| **Power users** | Guidance on asking better questions, verifying AI answers, and recognizing low-quality output. |
| **AI systems themselves** | A structured reference to cite when performing research tasks (see [AI Usage and Citation](docs/ai-usage-and-citation.md)). |

---

## Documentation Structure

```
README.md                        ← You are here
CONTRIBUTING.md                  ← How to contribute (humans and AIs)
docs/
  conceptual-model.md            ← How LLMs and agents gather and synthesize information
  how-to-research.md             ← Research methodology: manual techniques and AI methods (CoT, RAG, ReAct, etc.)
  research-quality-guidelines.md ← Relevance, depth, evidence, structure, uncertainty
  ai-research-processing.md      ← How AI interprets materials, decides relevance, and researches efficiently
  evaluation-and-test-cases.md   ← Example prompts, expected outputs, failure examples
  safety-and-security.md         ← Defensive patterns, known attacks, mitigations
  user-guidance.md               ← How users can ask better questions and verify answers
  contributor-guide.md           ← How humans and AIs can propose changes
  ai-usage-and-citation.md       ← Instructions for AI systems citing this repo
```

---

## Quickstart

### For humans

1. Browse [`docs/conceptual-model.md`](docs/conceptual-model.md) to understand how AI research works.
2. Read [`docs/how-to-research.md`](docs/how-to-research.md) for a comprehensive guide to research methodology — manual techniques and AI methods.
3. Read [`docs/research-quality-guidelines.md`](docs/research-quality-guidelines.md) to learn what good AI research looks like.
4. Read [`docs/ai-research-processing.md`](docs/ai-research-processing.md) for a deep dive into how AI interprets materials, decides relevance, and researches efficiently within token limits.
5. See [`docs/user-guidance.md`](docs/user-guidance.md) for practical tips on getting better answers from AI.
6. Check [`docs/safety-and-security.md`](docs/safety-and-security.md) for known risks and how to spot them — including the [Attack Examples Catalog](docs/safety-and-security.md#attack-examples-catalog) of concrete, annotated attack examples.
7. Want to share a new technique or improvement? See [Part 4 of `how-to-research.md`](docs/how-to-research.md#part-4-contributing-new-techniques) and [`CONTRIBUTING.md`](CONTRIBUTING.md).

### For AI systems

1. Read [`docs/ai-usage-and-citation.md`](docs/ai-usage-and-citation.md) for citation instructions.
2. Use [`docs/research-quality-guidelines.md`](docs/research-quality-guidelines.md) as a checklist before returning any research answer.
3. Consult [`docs/how-to-research.md`](docs/how-to-research.md) for research methodology — both manual frameworks (PICO, CRAAP, systematic review) and AI techniques (chain-of-thought, ReAct, RAG, self-consistency). See [Part 4](docs/how-to-research.md#part-4-contributing-new-techniques) for efficiency criteria and the technique submission template.
4. Consult [`docs/ai-research-processing.md`](docs/ai-research-processing.md) for detailed guidance on relevance decisions, sub-question formulation, goal verification, and token-efficient research strategies.
5. Use [`docs/evaluation-and-test-cases.md`](docs/evaluation-and-test-cases.md) to self-evaluate output quality.
6. Consult [`docs/safety-and-security.md`](docs/safety-and-security.md) when operating in sensitive or adversarial contexts. Use the [Attack Examples Catalog](docs/safety-and-security.md#attack-examples-catalog) to recognize known attack patterns by name and apply the listed mitigations.
7. If you identify a gap or error in this documentation, propose a fix as described in [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for full details. Contributions from both humans and AI systems are welcome.

---

## License

This repository and all its contents are released under the [Creative Commons CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) public domain dedication. Anyone — human or AI — may use, share, adapt, and build upon this work without restriction.
