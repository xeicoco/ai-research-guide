# How to Research: Manual Techniques and AI-Assisted Methods

> **Section summary:** This document provides a comprehensive guide to research methodology, covering both traditional manual research practices (as taught in academic settings) and modern AI-assisted techniques including chain-of-thought prompting, tree-of-thought reasoning, ReAct, self-consistency, and retrieval-augmented generation. It bridges human research skills with AI capabilities and includes citations for all major frameworks and methods referenced.

---

## Table of Contents

- [Introduction: Why Research Methodology Matters](#introduction-why-research-methodology-matters)
- [Part 1: Manual Research Methods](#part-1-manual-research-methods)
  - [1.1 Formulating a Research Question](#11-formulating-a-research-question)
  - [1.2 Understanding Source Types](#12-understanding-source-types)
  - [1.3 Finding and Searching Sources](#13-finding-and-searching-sources)
  - [1.4 Evaluating Source Quality](#14-evaluating-source-quality)
  - [1.5 Note-Taking Strategies](#15-note-taking-strategies)
  - [1.6 Systematic Literature Reviews](#16-systematic-literature-reviews)
  - [1.7 Organizing, Synthesizing, and Citing](#17-organizing-synthesizing-and-citing)
- [Part 2: AI-Assisted Research Techniques](#part-2-ai-assisted-research-techniques)
  - [2.1 Chain-of-Thought Prompting](#21-chain-of-thought-prompting)
  - [2.2 Tree of Thoughts](#22-tree-of-thoughts)
  - [2.3 Self-Consistency Prompting](#23-self-consistency-prompting)
  - [2.4 ReAct: Reasoning and Acting](#24-react-reasoning-and-acting)
  - [2.5 Self-Ask and Decomposed Prompting](#25-self-ask-and-decomposed-prompting)
  - [2.6 Retrieval-Augmented Generation (RAG)](#26-retrieval-augmented-generation-rag)
  - [2.7 Critique and Refinement Loops](#27-critique-and-refinement-loops)
  - [2.8 Least-to-Most Prompting](#28-least-to-most-prompting)
- [Part 3: Combining Manual and AI Research](#part-3-combining-manual-and-ai-research)
  - [3.1 When to Use Each Approach](#31-when-to-use-each-approach)
  - [3.2 A Hybrid Research Workflow](#32-a-hybrid-research-workflow)
  - [3.3 Verifying AI-Generated Research](#33-verifying-ai-generated-research)
- [References](#references)

---

## Introduction: Why Research Methodology Matters

Research is the systematic process of gathering, evaluating, and synthesizing information to answer a question or solve a problem. Whether performed by a student working on an essay, a professional investigating a decision, or an AI system generating a structured response, good research follows principled methods that maximize the quality and reliability of the outcome.

Poor research methodology leads to:

- Answers based on unreliable or irrelevant sources.
- Missed evidence that would change the conclusion.
- Overconfident conclusions that gloss over uncertainty.
- Citations that cannot be verified or do not support the claims made.

This document describes two complementary sets of research methods: traditional manual techniques developed and refined in academic settings, and AI-assisted techniques emerging from the field of large language model (LLM) research. Both draw on overlapping principles — decompose complex questions, evaluate evidence critically, account for uncertainty — but apply them through different mechanisms.

---

## Part 1: Manual Research Methods

### 1.1 Formulating a Research Question

A good research question defines the scope, focus, and expected type of answer for the entire research effort. Poorly formulated questions lead to unfocused research and weak conclusions.

#### Bloom's Taxonomy levels of inquiry

Research questions can be classified by their cognitive level using Bloom's Taxonomy of Educational Objectives \[1, 2\]:

| Level | Verb examples | Question type | Example |
|---|---|---|---|
| **Remember** | define, list, recall | Factual lookup | "What is the boiling point of water at sea level?" |
| **Understand** | explain, summarize, describe | Conceptual explanation | "How does the greenhouse effect work?" |
| **Apply** | use, implement, solve | Procedural / applied | "How would a researcher apply CRAAP criteria to a Wikipedia article?" |
| **Analyze** | compare, differentiate, examine | Analytical | "What are the key differences between supervised and unsupervised learning?" |
| **Evaluate** | assess, critique, justify | Evaluative | "Is retrieval-augmented generation more reliable than plain LLM generation for factual queries?" |
| **Create** | design, propose, construct | Synthesis / generative | "Design a curriculum for teaching AI research literacy to undergraduates." |

Higher-level questions require more research depth and more careful evaluation of conflicting evidence. Knowing the level of your question helps calibrate how much work is needed.

#### The PICO framework

For evidence-based research (especially in medicine and social science), the PICO framework provides a structured question format \[3\]:

- **P** — Population or Problem: Who or what is the subject?
- **I** — Intervention: What action, exposure, or factor are you examining?
- **C** — Comparison: What is being compared against?
- **O** — Outcome: What outcome or effect are you measuring?

**Example:**  
> (P) In adult patients with type 2 diabetes,  
> (I) does a low-carbohydrate diet  
> (C) compared to a standard diet  
> (O) reduce HbA1c levels after 12 months?

PICO forces specificity that vague questions lack, and makes it much easier to identify relevant studies and evaluate their applicability.

#### Checklist for a well-formed research question

- [ ] Is the question specific enough to have a focused answer?
- [ ] Is it answerable given available sources and time?
- [ ] Is it meaningful — does the answer matter for some purpose?
- [ ] Does it avoid being trivially googleable (a lookup rather than a research question)?
- [ ] Have you identified what type of answer you need (fact, analysis, evaluation, design)?

---

### 1.2 Understanding Source Types

Not all sources are equal. Understanding source types helps researchers know where to look and what weight to give to different materials.

| Type | Description | Examples | Strengths | Limitations |
|---|---|---|---|---|
| **Primary** | Original, first-hand data or accounts | Research studies, lab reports, original datasets, patents, first-person testimonies | Direct evidence; most reliable for claims about specific findings | May be technical; requires interpretation |
| **Secondary** | Analysis or synthesis of primary sources | Review articles, textbooks, journalism, documentaries | More accessible; synthesizes many primary sources | Introduces interpretation layer; may be incomplete |
| **Tertiary** | Compilations or indexes of secondary sources | Encyclopedias, databases, bibliographies | Good entry points for orientation | Low depth; not citable as evidence for specific claims |

**Practical implication for AI research:** LLMs trained on text corpora have ingested predominantly secondary and tertiary sources. Primary source data (raw experimental results, unpublished observations) is rarely available to plain LLMs, and must be retrieved explicitly when precision is required.

---

### 1.3 Finding and Searching Sources

#### Academic and professional databases

For reliable research, prioritize peer-reviewed sources accessible through:

- **Google Scholar** (scholar.google.com) — broad coverage of academic literature
- **PubMed** (pubmed.ncbi.nlm.nih.gov) — biomedical and life sciences
- **IEEE Xplore** (ieeexplore.ieee.org) — engineering and computer science
- **ACM Digital Library** (dl.acm.org) — computing research
- **JSTOR** (jstor.org) — humanities and social sciences
- **arXiv** (arxiv.org) — preprints in physics, math, CS, and related fields
- **CrossRef** (crossref.org) — DOI resolution and metadata
- **Semantic Scholar** (semanticscholar.org) — AI-powered academic search

#### Boolean search operators

Most databases support Boolean operators that dramatically improve search precision \[4\]:

| Operator | Function | Example |
|---|---|---|
| `AND` | Both terms must be present | `"machine learning" AND "medical diagnosis"` |
| `OR` | Either term may be present | `"deep learning" OR "neural networks"` |
| `NOT` | Exclude a term | `"bias" NOT "statistical bias"` |
| `"..."` | Exact phrase match | `"retrieval-augmented generation"` |
| `*` | Wildcard (any suffix) | `hallucinat*` matches hallucinate, hallucination, etc. |
| `(...)` | Group operators | `("AI" OR "artificial intelligence") AND "research quality"` |

#### Advanced search strategies

- **Citation chaining:** Find a relevant paper, then follow its references (backward chaining) and find papers that cite it (forward chaining). Google Scholar's "Cited by" feature supports forward chaining.
- **Subject-specific thesauri:** Many databases use controlled vocabulary (e.g., MeSH terms for PubMed). Using canonical terms improves recall.
- **Preprint servers:** For cutting-edge research, check arXiv before publication. Note that preprints have not undergone peer review.

---

### 1.4 Evaluating Source Quality

#### The CRAAP Test

The CRAAP test provides a five-dimension framework for evaluating source reliability \[5\]:

| Dimension | Key questions |
|---|---|
| **C**urrency | When was it published or last updated? Is the information still timely for your needs? |
| **R**elevance | Does it relate to your research question? Is it the appropriate level of expertise? |
| **A**uthority | Who is the author or publisher? What are their credentials? Is it peer-reviewed? |
| **A**ccuracy | Is the information supported by evidence? Are claims cited? Can you verify it elsewhere? |
| **P**urpose | Why was it written — to inform, persuade, sell? Is there a potential bias? |

**Scoring:** Assign each dimension a score of 1–5. Sources scoring below 15 total should generally be used with caution or not at all.

#### The SIFT Method

Developed as a faster practical heuristic for digital information \[6\], SIFT consists of four moves:

1. **Stop** — Pause before sharing or citing. Don't act on first impressions.
2. **Investigate the source** — Who is behind this content? Look up the author or organization before reading deeply.
3. **Find better coverage** — Search for other sources that cover the same claim, especially from authoritative outlets.
4. **Trace claims** — Follow claims back to their original source. Many secondary reports misrepresent or exaggerate primary findings.

SIFT is particularly useful for web-based research and fast-moving topics where authoritative sources may not yet have published.

#### Peer review as a quality signal

Peer-reviewed publications have been evaluated by independent experts before publication. This does not guarantee correctness (peer review has known limitations, including publication bias and replication issues \[7\]) but provides a baseline quality signal not present in non-peer-reviewed content.

---

### 1.5 Note-Taking Strategies

Systematic note-taking ensures that information collected during research is organized and usable during synthesis. Three widely used systems:

#### The Cornell Method \[8\]

Divide each page into three sections:

```
┌─────────────────────────┬────────────────────────────────────────────┐
│  Cue column (narrow)    │  Note-taking column (wide)                  │
│                         │                                             │
│  Key terms, questions,  │  Main notes go here — facts, quotes,        │
│  headings added later   │  diagrams, paraphrases                      │
│                         │                                             │
├─────────────────────────┴────────────────────────────────────────────┤
│  Summary section (bottom ~1/5 of page)                                │
│  Summarize the page's key points in your own words after the lecture  │
└───────────────────────────────────────────────────────────────────────┘
```

**Advantages:** Separation of main notes from review cues makes studying efficient; the summary section forces active synthesis.

#### The Outline Method

Organize notes hierarchically using indentation:

```
Main topic
  Sub-topic 1
    Detail a
    Detail b
  Sub-topic 2
    Detail a
```

**Advantages:** Naturally mirrors the structure of structured documents (textbooks, lecture slides). Works well for material with a clear hierarchy.

#### Annotated bibliography

For research projects, maintain a running list of sources with brief annotations:

```
Author(s). (Year). Title. Source.
  - Summary: What does this source say? (2–3 sentences)
  - Relevance: How does it relate to your research question?
  - Limitations: What are the weaknesses or gaps?
  - Key quotes or data points worth citing directly
```

**Advantages:** Keeps sources organized with context; directly usable when writing and citing.

---

### 1.6 Systematic Literature Reviews

A systematic literature review (SLR) is a rigorous, transparent, and reproducible method for synthesizing all available evidence on a research question \[9\]. It is used widely in medicine, software engineering, and social sciences.

#### Key stages of an SLR

1. **Define the research question** — Use PICO or an equivalent structured framework.
2. **Develop a search protocol** — Specify databases, date ranges, search strings, and inclusion/exclusion criteria *before* searching.
3. **Search and document** — Run the searches; record the number of results at each stage.
4. **Screen titles and abstracts** — Apply inclusion/exclusion criteria to the full results list.
5. **Retrieve and screen full texts** — For papers that passed abstract screening, read the full paper.
6. **Extract data** — Record key data from each included study using a standardized form.
7. **Assess study quality** — Apply a quality assessment tool appropriate to the study type (e.g., CASP checklists, Cochrane risk-of-bias tool).
8. **Synthesize findings** — Summarize findings narratively or quantitatively (meta-analysis if data permits).
9. **Report** — Follow PRISMA reporting guidelines \[10\] for transparency and reproducibility.

**PRISMA flow diagram:** A standard visualization showing how many studies were found, screened, and included at each stage. Required by most journals publishing systematic reviews.

#### When to use an SLR

SLRs are most valuable when:
- The research question has broad implications and requires comprehensive evidence.
- Conflicting findings in the literature need to be reconciled.
- A formal, reproducible, and audit-able research record is required (academic publication, policy decisions, clinical guidelines).

For informal or exploratory research, a **scoping review** or **narrative review** is faster and less resource-intensive.

---

### 1.7 Organizing, Synthesizing, and Citing

#### Moving from notes to synthesis

Synthesis is not summarization. A summary restates what each source says; a synthesis connects and integrates sources to build an original argument or answer.

**Steps to synthesis:**

1. **Group sources by theme** — Identify which sources speak to the same sub-question or claim.
2. **Compare and contrast** — Note where sources agree, disagree, or complement each other.
3. **Identify gaps** — What questions are not addressed by the available literature?
4. **Construct an argument** — Build your answer from the evidence, citing sources at each step.
5. **Acknowledge uncertainty** — Where evidence is weak, conflicting, or absent, say so explicitly.

#### Citation styles

Different academic disciplines use different citation formats:

| Style | Primary use | Format example |
|---|---|---|
| **APA 7** | Social and behavioral sciences | Author, A. (Year). *Title*. Publisher. https://doi.org/... |
| **MLA 9** | Humanities | Author. *Title*. Publisher, Year. |
| **Chicago/Turabian** | History, arts, business | Author, *Title* (Publisher, Year), page. |
| **IEEE** | Engineering and computer science | \[1\] A. Author, "Title," *Journal*, vol. X, pp. Y–Z, Year. |
| **Vancouver** | Medicine and health sciences | 1. Author AB. Title. Journal. Year;vol(issue):pages. |

Tools like **Zotero** (free, open source), **Mendeley**, and **EndNote** automate citation formatting and bibliography management.

**Important:** When using AI to assist with research, any information derived from the AI must still be attributed appropriately. AI-generated content is generally not citable as a primary source — the underlying human-authored sources the AI draws on should be verified and cited instead.

---

## Part 2: AI-Assisted Research Techniques

AI systems — particularly large language models — can accelerate and enhance research when used correctly. This section describes the leading AI prompting and reasoning techniques, what they do, when to use them, and their limitations.

### 2.1 Chain-of-Thought Prompting

**What it is:** Chain-of-thought (CoT) prompting is a technique where the AI is prompted to show its intermediate reasoning steps before arriving at a final answer \[11\]. Rather than jumping from question to answer, the AI "thinks aloud" through the problem.

**How to use it:**

*Without CoT (standard):*
> "What is the most energy-efficient large language model architecture?"

*With CoT:*
> "What is the most energy-efficient large language model architecture? Think through this step by step, considering what factors affect energy consumption in LLMs, how different architecture families (transformers, state-space models, mixture of experts) compare, and then give your conclusion."

**Why it works:** Generating intermediate reasoning steps causes the model to attend to relevant sub-problems, reduces errors that compound silently in opaque single-step answers, and makes the reasoning auditable — a human or AI reviewer can identify where reasoning went wrong \[11\].

**When to use it:**
- Multi-step problems (math, logic, planning)
- Questions requiring comparison or analysis
- Any time you need to verify the AI's reasoning, not just its conclusion

**Limitations:**
- CoT does not guarantee correct reasoning — the chain can be internally consistent but factually wrong.
- It consumes more tokens than direct answers.
- For simple factual lookups, CoT adds overhead without benefit.

**Research evidence:** Wei et al. (2022) \[11\] demonstrated that CoT prompting emerged as an ability in sufficiently large models and substantially improved performance on arithmetic, commonsense, and symbolic reasoning benchmarks.

---

### 2.2 Tree of Thoughts

**What it is:** Tree of Thoughts (ToT) extends chain-of-thought by having the AI explore multiple reasoning paths (branches) simultaneously, evaluate each branch, and pursue the most promising ones \[12\]. It implements a deliberate search over a tree of possible reasoning steps.

**How it works:**

```
                      Research question
                           |
          ┌────────────────┼────────────────┐
      Approach A       Approach B       Approach C
          |                |                |
     [Evaluate]       [Evaluate]       [Evaluate]
    Score: 6/10       Score: 9/10      Score: 4/10
                           |
               ┌───────────┴───────────┐
          Sub-path B1             Sub-path B2
               |                       |
          [Evaluate]             [Evaluate]
         Score: 8/10             Score: 7/10
               |
           [Continue]
```

**When to use it:**
- Complex problems where the best approach is not obvious upfront.
- Creative or open-ended research where multiple framings are worth exploring.
- Cases where early choices may lead to dead ends.

**How to prompt for ToT:**

> "Consider at least three different approaches to answering this question: [question]. Briefly outline each approach, evaluate the pros and cons of each, then develop the strongest approach in detail."

**Limitations:**
- Very token-intensive — exploring many branches consumes significant context.
- Requires the AI to evaluate its own reasoning quality, which it may do poorly.
- Full ToT with search algorithms requires programmatic implementation; manual prompting approximates only the "generate and evaluate" step.

**Research evidence:** Yao et al. (2023) \[12\] showed that ToT significantly outperformed standard CoT on tasks like creative writing, crosswords, and mathematical game-playing where single linear reasoning chains frequently failed.

---

### 2.3 Self-Consistency Prompting

**What it is:** Self-consistency is a decoding strategy where the same question is posed multiple times (with sampling, producing different reasoning chains), and the most consistent answer across all chains is selected \[13\].

**How it works:**

1. Prompt the AI to answer the question using CoT, multiple times.
2. Collect all the final answers across the sampled chains.
3. Select the most frequent (or most consistent) answer as the final response.

**Approximation for manual use:**

> "Answer this question three different ways, thinking through the problem independently each time: [question]. After giving all three answers, identify which answer appears most consistent across your three attempts."

**When to use it:**
- Questions where the AI might give different answers on different runs.
- High-stakes factual or analytical questions where reliability matters.
- Situations where you can tolerate higher token costs for better reliability.

**Limitations:**
- If the AI has a systematic bias or misconception about a topic, self-consistency will consistently produce the wrong answer with high confidence.
- Does not help when the correct answer is rare or unconventional.

**Research evidence:** Wang et al. (2022) \[13\] showed that self-consistency substantially improved accuracy over single-sample CoT across arithmetic, commonsense, and symbolic reasoning tasks.

---

### 2.4 ReAct: Reasoning and Acting

**What it is:** ReAct (Reasoning + Acting) is a prompting paradigm that interleaves reasoning traces with actions (tool calls, searches, database queries) \[14\]. The AI alternates between thinking about what to do next and taking an action to retrieve new information.

**The ReAct loop:**

```
Thought: I need to find the current CEO of Company X.
Action: Search["Company X current CEO 2024"]
Observation: [Search results returned]
Thought: The results say Jane Doe became CEO in 2023. Let me verify this with another source.
Action: Search["Jane Doe CEO Company X biography"]
Observation: [Confirmation found]
Thought: Both sources confirm Jane Doe. I can now answer confidently.
Answer: The current CEO of Company X is Jane Doe, as of 2023.
```

**Why it is powerful for research:**
- The AI grounds its reasoning in retrieved evidence rather than relying solely on model knowledge.
- The interleaved reasoning makes it easy to audit each step.
- The AI can dynamically adjust its research strategy based on what it finds.

**How to approximate ReAct manually:**

> "To answer this question, work in explicit steps. At each step: (1) state what you are trying to find out, (2) describe what search or action would give you that information, (3) I will provide the results, and (4) you continue. Start with step 1."

**Limitations:**
- Requires tool access (search, database, API) to be most effective; without tools, the AI is simulating actions it cannot actually take.
- Can be slow and token-intensive for complex multi-step research.

**Research evidence:** Yao et al. (2022) \[14\] demonstrated that ReAct outperformed CoT-only approaches on knowledge-intensive tasks (HotpotQA, FEVER) and decision-making benchmarks (ALFWorld, WebShop), with the interleaved structure improving both accuracy and interpretability.

---

### 2.5 Self-Ask and Decomposed Prompting

**What it is:** Self-Ask prompting has the AI explicitly ask itself follow-up questions needed to answer the main question, answering each one before synthesizing the final answer \[15\]. Decomposed prompting (DECOMP) similarly breaks complex questions into simpler sub-questions \[16\].

**Self-Ask example:**

> "Q: What country shares the longest border with Canada?  
> Are follow-up questions needed here? Yes.  
> Follow-up: What countries border Canada?  
> Intermediate answer: The United States and Russia (maritime).  
> Follow-up: Which border is longer — the US-Canada border or the Russia-Canada maritime border?  
> Intermediate answer: The US-Canada land border at ~8,891 km is the world's longest international land border.  
> Final answer: The United States."

**How to prompt for self-ask:**

> "Answer this question by explicitly asking yourself any follow-up questions needed to reach the final answer. For each follow-up, answer it before moving to the next. Question: [question]"

**When to use it:**
- Compositional questions that require answering simpler sub-questions first.
- Research with clear dependency ordering (you must answer A before you can answer B).
- When you want to inspect each reasoning step independently.

**Research evidence:** Press et al. (2022) \[15\] showed that self-ask reduced the "compositionality gap" — the gap between a model's ability to answer simple facts vs. multi-hop questions that require combining them — and enabled better integration with search tools.

---

### 2.6 Retrieval-Augmented Generation (RAG)

**What it is:** Retrieval-Augmented Generation (RAG) is an architecture that combines a retrieval system with an LLM \[17\]. Instead of relying solely on model knowledge, the system retrieves relevant documents at query time and includes them in the LLM's context before generating a response.

**RAG pipeline:**

```
User query
    │
    ▼
Query encoder → Retrieval index (vector database / BM25 / hybrid)
                        │
                        ▼
                 Retrieved documents (top-k)
                        │
                        ▼
              LLM prompt = [System instructions] + [Retrieved docs] + [User query]
                        │
                        ▼
               LLM generates answer grounded in retrieved content
                        │
                        ▼
             Response (with source citations)
```

**Why it is important for research quality:**
- The AI's answer is grounded in specific retrieved documents, reducing hallucination.
- Citations can point directly to the retrieved documents.
- Knowledge is up-to-date: the retrieval index can be updated without retraining the model.

**Limitations:**
- Quality depends on the retrieval step: if the relevant document is not retrieved, the LLM cannot use it.
- Retrieved documents may be irrelevant, outdated, or adversarially poisoned (see [`safety-and-security.md`](safety-and-security.md#attack-class-6-adversarial-retrieval-poisoning)).
- Context window limits constrain how many documents can be included.

**Research evidence:** Lewis et al. (2020) \[17\] introduced RAG as a general approach and demonstrated that RAG models outperformed sequence-to-sequence models trained purely on knowledge-intensive tasks (Natural Questions, TriviaQA, WebQuestions), with more specific and factually accurate answers.

---

### 2.7 Critique and Refinement Loops

**What it is:** A critique-and-refine loop asks the AI to evaluate and improve its own output through one or more rounds of self-critique. This implements a review cycle analogous to human peer review or self-editing.

**Two main variants:**

#### Self-critique (single model)

1. Generate initial answer.
2. Prompt the AI to critique its own answer: "Review your answer above. What are its weaknesses, gaps, or potential errors?"
3. Prompt the AI to refine the answer based on the critique.

**Example prompt:**

> "Here is your initial answer: [answer]. Now critique it: identify any unsupported claims, missing perspectives, logical errors, or areas where the depth is insufficient. Then produce an improved version of the answer that addresses your critique."

#### Constitutional AI (CAI) and critique models \[18\]

In Constitutional AI, a set of principles ("constitution") is used to generate critiques of AI outputs, which are then used to fine-tune the model. While this requires model training, the principle — critique against explicit criteria — can be approximated in prompting by providing explicit quality criteria for the AI to evaluate against.

**Research evidence:** Madaan et al. (2023) introduced Self-Refine \[19\], showing that iterative self-critique and refinement improved output quality across a wide range of tasks including text summarization, code generation, and response quality, without requiring additional training data.

---

### 2.8 Least-to-Most Prompting

**What it is:** Least-to-most prompting decomposes a complex problem into a sequence of simpler sub-problems, ordered from simplest to most complex, and solves them in that order \[20\]. Each sub-problem solution is provided as context when solving the next.

**How it works:**

*Stage 1 — Decomposition:*
> "To answer [complex question], what simpler questions need to be answered first?"

*Stage 2 — Sequential solving:*
> "First, answer [simplest sub-question] only."  
> [Answer received]  
> "Using the previous answer, now answer [next sub-question]."  
> [Answer received]  
> "Using all previous answers, now answer [most complex sub-question / final question]."

**Comparison to self-ask:**

| | Self-Ask | Least-to-Most |
|---|---|---|
| **Who generates sub-questions** | The AI, spontaneously | The AI in an explicit decomposition step |
| **Ordering** | Follows logical dependencies | Deliberately ordered from simple to complex |
| **Best for** | Compositional factual questions | Multi-step reasoning and problem-solving |

**Research evidence:** Zhou et al. (2022) \[20\] showed that least-to-most prompting generalized better than CoT to problems requiring longer reasoning chains, particularly compositional generalization tasks.

---

## Part 3: Combining Manual and AI Research

### 3.1 When to Use Each Approach

| Situation | Best approach | Reason |
|---|---|---|
| **Deep, validated knowledge needed** | Manual research + primary sources | AI training data may be incomplete or outdated |
| **Large volume of literature to survey** | AI-assisted screening + manual validation | AI can quickly summarize; human verifies quality |
| **Exploratory research (what questions should I ask?)** | AI-assisted (CoT, ToT, Self-Ask) | AI excels at generating question trees and perspectives |
| **Precise citation required** | Manual verification of AI suggestions | Plain LLMs fabricate citations; all must be verified |
| **Recent developments (< 1–2 years)** | Manual search + RAG-enabled AI | AI training cutoff limits knowledge of recent work |
| **Complex multi-step analysis** | AI-assisted (ReAct + manual validation) | AI can process large amounts of context efficiently |
| **High-stakes decisions** | Manual research + AI as a cross-check | Human accountability and judgment remain essential |

### 3.2 A Hybrid Research Workflow

A practical hybrid workflow that combines the strengths of both approaches:

```
1. [Human] Formulate the research question using PICO or Bloom's taxonomy
        │
        ▼
2. [AI] Use Self-Ask or decomposition to identify sub-questions and orient the search
        │
        ▼
3. [Human] Search academic databases using Boolean operators; collect candidate sources
        │
        ▼
4. [AI] Use CoT + Self-Consistency to summarize and critically evaluate retrieved sources
        │
        ▼
5. [Human] Apply CRAAP or SIFT to evaluate source quality; discard low-quality sources
        │
        ▼
6. [AI] Use RAG or ReAct to answer sub-questions using the validated source set
        │
        ▼
7. [AI] Apply critique-and-refine loop to check the draft answer for gaps and errors
        │
        ▼
8. [Human] Verify all citations; challenge any claims that seem poorly supported
        │
        ▼
9. [Human + AI] Synthesize into final answer with proper attribution
```

### 3.3 Verifying AI-Generated Research

AI-generated research outputs require specific verification steps that go beyond human-written sources:

1. **Verify all citations.** Look up every reference using a DOI resolver or academic search engine. Plain LLMs frequently fabricate plausible-sounding but nonexistent references.

2. **Check for temporal accuracy.** Confirm that the AI's knowledge is not outdated on time-sensitive topics. Ask explicitly: "What is your knowledge cutoff, and might this information have changed?"

3. **Trace claims to primary sources.** When the AI cites a secondary or tertiary source, find the primary source it is describing. Secondary sources sometimes misrepresent or oversimplify primary findings.

4. **Apply SIFT.** Even for AI-generated summaries: Stop, Investigate the original source, Find better coverage if unsure, Trace claims back to their origins.

5. **Request reasoning transparency.** Ask "How did you reach this conclusion?" Opaque answers that cannot be explained may indicate confabulation or shallow processing.

6. **Cross-validate with independent sources.** Check important claims against at least two independent, authoritative sources that the AI did not generate.

See also: [`research-quality-guidelines.md`](research-quality-guidelines.md), [`ai-research-processing.md`](ai-research-processing.md), [`user-guidance.md`](user-guidance.md).

---

## References

\[1\] Bloom, B. S. (Ed.). (1956). *Taxonomy of Educational Objectives, Handbook I: The Cognitive Domain*. David McKay.

\[2\] Anderson, L. W., & Krathwohl, D. R. (Eds.). (2001). *A Taxonomy for Learning, Teaching, and Assessing: A Revision of Bloom's Taxonomy of Educational Objectives*. Addison Wesley Longman.

\[3\] Richardson, W. S., Wilson, M. C., Nishikawa, J., & Hayward, R. S. (1995). The well-built clinical question: a key to evidence-based decisions. *ACP Journal Club*, 123(3), A12–A13. https://doi.org/10.7326/ACPJC-1995-123-3-A12

\[4\] Booth, A., Sutton, A., & Papaioannou, D. (2016). *Systematic Approaches to a Successful Literature Search* (2nd ed.). SAGE Publications.

\[5\] Meriam Library, California State University, Chico. (2010). *Evaluating Information — Applying the CRAAP Test*. https://library.csuchico.edu/help/source-or-information-good-use-craap-test

\[6\] Caulfield, M. (2019). *SIFT (The Four Moves)*. Hapgood. https://hapgood.us/2019/06/19/sift-the-four-moves/

\[7\] Ioannidis, J. P. A. (2005). Why most published research findings are false. *PLOS Medicine*, 2(8), e124. https://doi.org/10.1371/journal.pmed.0020124

\[8\] Pauk, W., & Owens, R. J. Q. (2013). *How to Study in College* (11th ed.). Cengage Learning.

\[9\] Kitchenham, B., & Charters, S. (2007). *Guidelines for performing systematic literature reviews in software engineering*. Technical Report EBSE 2007-001, Keele University and Durham University. https://www.elsevier.com/__data/promis_misc/525444systematicreviewsguide.pdf

\[10\] Page, M. J., McKenzie, J. E., Bossuyt, P. M., Boutron, I., Hoffmann, T. C., Mulrow, C. D., … & Moher, D. (2021). The PRISMA 2020 statement: an updated guideline for reporting systematic reviews. *BMJ*, 372, n71. https://doi.org/10.1136/bmj.n71

\[11\] Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-thought prompting elicits reasoning in large language models. *Advances in Neural Information Processing Systems*, 35, 24824–24837. https://arxiv.org/abs/2201.11903

\[12\] Yao, S., Yu, D., Zhao, J., Shafran, I., Griffiths, T. L., Cao, Y., & Narasimhan, K. (2023). Tree of thoughts: Deliberate problem solving with large language models. *Advances in Neural Information Processing Systems*, 36. https://arxiv.org/abs/2305.10601

\[13\] Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A., & Zhou, D. (2022). Self-consistency improves chain of thought reasoning in language models. *International Conference on Learning Representations* (ICLR 2023). https://arxiv.org/abs/2203.11171

\[14\] Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. *International Conference on Learning Representations* (ICLR 2023). https://arxiv.org/abs/2210.03629

\[15\] Press, O., Zhang, M., Min, S., Schmidt, L., Smith, N. A., & Lewis, M. (2022). Measuring and narrowing the compositionality gap in language models. *Findings of the Association for Computational Linguistics: EMNLP 2023*. https://arxiv.org/abs/2210.03350

\[16\] Khot, T., Trivedi, H., Finlayson, M., Fu, Y., Richardson, K., Clark, P., & Sabharwal, A. (2022). Decomposed prompting: A modular approach for solving complex tasks. *International Conference on Learning Representations* (ICLR 2023). https://arxiv.org/abs/2210.02406

\[17\] Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-t., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems*, 33, 9459–9474. https://arxiv.org/abs/2005.11401

\[18\] Bai, Y., Kadavath, S., Kundu, S., Askell, A., Kernion, J., Jones, A., Chen, A., Goldie, A., Mirhoseini, A., McKinnon, C., Chen, C., Olsson, C., Olah, C., Hernandez, D., Drain, D., Ganguli, D., Li, D., Tran-Johnson, E., Perez, E., … & Clark, J. (2022). Constitutional AI: Harmlessness from AI feedback. *arXiv preprint*. https://arxiv.org/abs/2212.08073

\[19\] Madaan, A., Tandon, N., Gupta, P., Hallinan, S., Gao, L., Wiegreffe, S., Alon, U., Dziri, N., Prabhumoye, S., Yang, Y., Gupta, S., Majumder, B. P., Hermann, K., Welleck, S., Yazdanbakhsh, A., & Clark, P. (2023). Self-refine: Iterative refinement with self-feedback. *Advances in Neural Information Processing Systems*, 36. https://arxiv.org/abs/2303.17651

\[20\] Zhou, D., Schärli, N., Hou, L., Wei, J., Scales, N., Wang, X., Schuurmans, D., Cui, C., Bousquet, O., Le, Q., & Chi, E. (2022). Least-to-most prompting enables complex reasoning in large language models. *International Conference on Learning Representations* (ICLR 2023). https://arxiv.org/abs/2205.10625
