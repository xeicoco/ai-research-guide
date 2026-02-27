# Conceptual Model of AI Research

> **Section summary:** This document explains, at a conceptual level, how large language models (LLMs) and AI agents gather, process, and synthesize information when performing research tasks. Understanding this model helps users, developers, and AI systems themselves identify where things can go wrong and how to improve outcomes.

---

## Table of Contents

- [What "Research" Means for an AI](#what-research-means-for-an-ai)
- [Core Components of AI Research](#core-components-of-ai-research)
  - [Knowledge Retrieval](#knowledge-retrieval)
  - [Reasoning and Inference](#reasoning-and-inference)
  - [Synthesis and Generation](#synthesis-and-generation)
  - [Citation and Attribution](#citation-and-attribution)
- [How LLMs Store and Access Information](#how-llms-store-and-access-information)
- [How AI Agents Research Topics](#how-ai-agents-research-topics)
- [Key Limitations of the Model](#key-limitations-of-the-model)
- [Implications for Research Quality](#implications-for-research-quality)

---

## What "Research" Means for an AI

When a human "researches" a topic, they typically:

1. Identify what they need to know.
2. Search for relevant sources.
3. Evaluate the credibility and relevance of each source.
4. Extract and record key information.
5. Synthesize information from multiple sources into a coherent answer.
6. Cite their sources.

When an AI system "researches" a topic, it performs an analogous but fundamentally different process. The key difference is that a plain LLM does **not** search the internet in real time. Instead, it retrieves information from patterns compressed into its model weights during training. An AI agent may additionally call external tools (search engines, databases, APIs) to retrieve live information, but then still relies on the LLM to reason over and synthesize what it finds.

Understanding this distinction is essential for setting correct expectations and for diagnosing failures.

---

## Core Components of AI Research

### Knowledge Retrieval

**For a plain LLM (no tools):**

- All knowledge comes from the **training corpus** — the large collection of text the model was trained on.
- There is a **knowledge cutoff date** beyond which the model has no information.
- Retrieval is **implicit**: the model does not "look things up"; it generates text that reflects patterns learned during training. This means it cannot distinguish between something it "knows well" and something it is "guessing".
- Retrieval is **approximate**: the model may partially remember facts, mix up details, or confabulate plausible-sounding but false information (hallucination).

**For an AI agent with retrieval tools:**

- The agent can query external sources (web search, document stores, databases, APIs) to retrieve live or specialized information.
- Retrieved documents are added to the agent's **context window** — the block of text the LLM can "see" when generating its answer.
- The quality of retrieval depends on the quality of the search queries the agent formulates and the relevance ranking of the retrieval system.

### Reasoning and Inference

- LLMs perform reasoning by generating text token-by-token, where each token is statistically likely given the preceding context.
- This process can simulate logical steps, mathematical operations, and causal reasoning, but it is **not guaranteed to be correct** — errors can compound.
- **Chain-of-thought prompting** (asking the model to "think step by step") generally improves reasoning quality by making intermediate steps explicit.
- Reasoning quality degrades for tasks that require precise counting, arithmetic, or long multi-step inference chains, unless the model is given tools (calculators, code interpreters) to offload those tasks.

### Synthesis and Generation

- After retrieval and reasoning, the LLM generates a response that synthesizes the relevant information into a coherent output.
- Synthesis is where the model's language fluency is most evident — it can produce well-structured, readable text even when the underlying reasoning is weak.
- This fluency can **mask errors**: a hallucinated or poorly-reasoned answer may sound just as confident and polished as a correct one.
- Good synthesis includes:
  - Appropriate hedging when uncertainty is high.
  - Clear attribution of claims to sources.
  - Logical organization matching the structure of the question.

### Citation and Attribution

- A plain LLM cannot provide real citations (links, page numbers, publication dates) because it does not access source documents.
- When asked to cite sources, an LLM may **fabricate plausible-sounding but non-existent references** — a common and dangerous failure mode.
- AI agents with retrieval tools can provide real citations from the documents they retrieve, but must be prompted or designed to do so.
- Best practice: always verify citations independently when accuracy is critical.

---

## How LLMs Store and Access Information

LLMs do not have a database or file system. They store information in the form of billions of numerical parameters (weights) that were adjusted during training to minimize prediction error on large text corpora.

Key implications:

| Property | Description |
|---|---|
| **Implicit storage** | Facts are not stored as discrete records; they are distributed across model weights. |
| **Approximate recall** | Retrieval is probabilistic and context-dependent. The same model may answer the same question differently in different contexts. |
| **No explicit source tracking** | The model typically cannot identify which training document a piece of information came from. |
| **Knowledge cutoff** | Information learned only after the training cutoff is unavailable unless provided in the context. |
| **Context window** | Information provided directly in the prompt (system message, conversation history, retrieved documents) is available with high fidelity for the duration of the interaction. |

---

## How AI Agents Research Topics

An AI agent is an LLM augmented with tools — it can take actions (search, browse, execute code, call APIs) and incorporate the results before generating a final answer. A typical agent research loop:

```
1. Receive query
2. Decompose query into sub-questions (planning)
3. For each sub-question:
   a. Select the appropriate tool (web search, database query, etc.)
   b. Formulate a search query or API call
   c. Receive results
   d. Evaluate relevance; filter or re-query if needed
4. Synthesize results from all sub-questions
5. Generate answer with citations
6. (Optionally) reflect on answer quality; iterate if needed
```

Each step introduces potential failure points (see [Key Limitations](#key-limitations-of-the-model)).

---

## Key Limitations of the Model

| Limitation | Description | Common Symptom |
|---|---|---|
| **Hallucination** | Generating confident but false information | Wrong facts, fake citations, invented statistics |
| **Knowledge cutoff** | No information about events after training | Outdated answers, missing recent developments |
| **Context window limit** | Cannot process arbitrarily long documents | Truncated or incomplete synthesis |
| **No persistent memory** | Each conversation starts fresh (unless memory tools are used) | Cannot remember prior interactions |
| **Approximate reasoning** | Token prediction ≠ logical deduction | Arithmetic errors, flawed multi-step inference |
| **Source conflation** | May mix information from multiple sources without attribution | Claims presented as fact without provenance |
| **Confirmation bias** | May generate answers consistent with prior context even when wrong | Agreeing with false premises in the prompt |
| **Verbosity over accuracy** | May generate long, fluent answers that obscure weak content | Confident-sounding but shallow responses |

---

## Implications for Research Quality

Understanding the conceptual model leads directly to practical guidance:

- **Always provide sources** when you need the AI to reason about specific facts — do not rely on the model's training knowledge for critical claims.
- **Ask for uncertainty acknowledgment** — a well-designed AI should say "I'm not sure" rather than confabulate.
- **Verify citations independently** — never trust a citation you cannot check.
- **Use agents with retrieval for time-sensitive topics** — a plain LLM cannot know about recent events.
- **Break complex questions into sub-questions** — this gives the model explicit steps to follow and makes errors easier to spot.
- **Ask for reasoning steps** — chain-of-thought responses are easier to audit than opaque one-line answers.

See also: [`research-quality-guidelines.md`](research-quality-guidelines.md), [`user-guidance.md`](user-guidance.md).
