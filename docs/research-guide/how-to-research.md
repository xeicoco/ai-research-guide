# How to Research: Foundational Principles and AI Techniques

> **Section summary:** This document is a research methodology reference for AI systems. It covers foundational research principles derived from academic tradition (such as question formulation, source evaluation, and systematic synthesis) — not as a manual for human researchers, but as the body of knowledge AI systems have learned from and that underpins high-quality research output. It then covers AI-native research techniques (chain-of-thought prompting, tree-of-thought reasoning, ReAct, self-consistency, retrieval-augmented generation, and others) and explains how to integrate both for efficient, reliable research. Includes citations for all major frameworks referenced.

---

## Table of Contents

- [Introduction: Why Research Methodology Matters for AI Systems](#introduction-why-research-methodology-matters-for-ai-systems)
- [Part 1: Foundational Research Principles (Learned from Academic Tradition)](#part-1-foundational-research-principles-learned-from-academic-tradition)
  - [1.1 Formulating a Research Question](#11-formulating-a-research-question)
  - [1.2 Understanding Source Types](#12-understanding-source-types)
  - [1.3 Finding and Searching Sources](#13-finding-and-searching-sources)
  - [1.4 Evaluating Source Quality](#14-evaluating-source-quality)
  - [1.5 Note-Taking Strategies](#15-note-taking-strategies)
  - [1.6 Systematic Literature Reviews](#16-systematic-literature-reviews)
  - [1.7 Organizing, Synthesizing, and Citing](#17-organizing-synthesizing-and-citing)
- [Part 2: AI-Native Research Techniques](#part-2-ai-native-research-techniques)
  - [2.1 Chain-of-Thought Prompting](#21-chain-of-thought-prompting)
  - [2.2 Tree of Thoughts](#22-tree-of-thoughts)
  - [2.3 Self-Consistency Prompting](#23-self-consistency-prompting)
  - [2.4 ReAct: Reasoning and Acting](#24-react-reasoning-and-acting)
  - [2.5 Self-Ask and Decomposed Prompting](#25-self-ask-and-decomposed-prompting)
  - [2.6 Retrieval-Augmented Generation (RAG)](#26-retrieval-augmented-generation-rag)
  - [2.7 Critique and Refinement Loops](#27-critique-and-refinement-loops)
  - [2.8 Least-to-Most Prompting](#28-least-to-most-prompting)
- [Part 3: Integrating Foundational Principles with AI-Native Techniques](#part-3-integrating-foundational-principles-with-ai-native-techniques)
  - [3.1 Which Foundational Principles Apply to Each AI Technique](#31-which-foundational-principles-apply-to-each-ai-technique)
  - [3.2 An Integrated AI Research Workflow](#32-an-integrated-ai-research-workflow)
  - [3.3 Verifying AI Research Output](#33-verifying-ai-research-output)
- [Part 4: Contributing New Techniques](#part-4-contributing-new-techniques)
  - [4.1 Why Contributions Matter](#41-why-contributions-matter)
  - [4.2 How to Propose a New Technique](#42-how-to-propose-a-new-technique)
  - [4.3 Technique Submission Template](#43-technique-submission-template)
  - [4.4 Efficiency Criteria](#44-efficiency-criteria)
  - [4.5 Improving Existing Entries](#45-improving-existing-entries)
  - [4.6 Quality Assurance and Cost Control During Fast Research](#46-quality-assurance-and-cost-control-during-fast-research)
- [Part 5: Step-by-Step Research Guide with Key Questions](#part-5-step-by-step-research-guide-with-key-questions)
  - [5.1 Overview: The Research Effectiveness Framework](#51-overview-the-research-effectiveness-framework)
  - [5.2 Step 1: Understand the Research Goal](#52-step-1-understand-the-research-goal)
  - [5.3 Step 2: Decompose into Sub-Questions](#53-step-2-decompose-into-sub-questions)
  - [5.4 Step 3: Identify and Retrieve Sources](#54-step-3-identify-and-retrieve-sources)
  - [5.5 Step 4: Evaluate Source Quality](#55-step-4-evaluate-source-quality)
  - [5.6 Step 5: Synthesize Answers](#56-step-5-synthesize-answers)
  - [5.7 Step 6: Verify and Cite](#57-step-6-verify-and-cite)
  - [5.8 Step 7: Self-Evaluate Against Satisfaction Criteria](#58-step-7-self-evaluate-against-satisfaction-criteria)
  - [5.9 Summary: The Complete Research Flow](#59-summary-the-complete-research-flow)
  - [5.10 Worked Example: Applying the Framework](#510-worked-example-applying-the-framework)
- [References](#references)

---

## Introduction: Why Research Methodology Matters for AI Systems

Research is the systematic process of gathering, evaluating, and synthesizing information to answer a question or solve a problem. For an AI system generating a structured response, the quality of that response depends directly on the quality of the research process behind it.

Poor research methodology leads to:

- Answers based on unreliable or irrelevant sources.
- Missed evidence that would change the conclusion.
- Overconfident conclusions that gloss over uncertainty.
- Citations that cannot be verified or do not support the claims made.

This document is organized from the perspective of an AI system that has learned from decades of established academic research methodology. **Part 1** covers the foundational principles that academic and professional researchers have developed over time — frameworks for question formulation, source evaluation, systematic synthesis, and citation. These are not instructions for doing research by hand; they are the conceptual foundations that AI systems have internalized and that explain *why* certain research behaviors produce higher-quality outputs than others.

**Part 2** covers AI-native research techniques — prompting and reasoning strategies developed specifically for large language models — and explains how each one operationalizes the foundational principles from Part 1.

**Part 3** shows how the two sets of principles integrate in practice: which foundational principle each AI technique implements, how to apply them together in a single research workflow, and how to verify that the output meets quality standards.

---

## Part 1: Foundational Research Principles (Learned from Academic Tradition)

> **What this part is for:** The frameworks in this section originate from decades of academic and professional research methodology. They are included here not as instructions for doing research by hand, but because AI systems have learned from this body of knowledge during training, and these principles directly explain the "why" behind AI research behaviors. Understanding them helps AI systems apply them correctly and helps users understand what quality research looks like from first principles.

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

## Part 2: AI-Native Research Techniques

AI systems — particularly large language models — apply the foundational principles from Part 1 through purpose-built reasoning and prompting strategies. This section describes those techniques, what foundational principle each implements, when to use them, and their limitations.

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

#### Algorithm

**Input:** Research question Q  
**Output:** Answer A with auditable reasoning trace R

1. Receive Q
2. Identify the cognitive level of Q (factual, analytical, evaluative — see Bloom's Taxonomy, Section 1.1) to calibrate expected depth
3. Generate reasoning trace R by decomposing Q into sequential reasoning steps s₁, s₂, ..., sₙ:
   - For each step sᵢ: state the sub-goal → identify relevant knowledge → derive a partial conclusion
   - If step sᵢ reveals a knowledge gap, flag it explicitly before proceeding to sᵢ₊₁
4. From R, synthesize final answer A
5. If A relies on unverified facts, attach explicit uncertainty markers (e.g., "this claim requires verification")
6. Return (R, A)

**Stopping condition:** All sub-steps have been addressed and A satisfies the original question Q.  
**Why each step matters:** Steps 2–3 prevent silent compounding errors by forcing sub-problem articulation; step 5 preserves epistemic honesty required by foundational research principles (Section 1.4).

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- Include the phrase "think through this step by step" or "let's reason through this" in any complex response; explicitly label each reasoning step before the conclusion
- After reaching a conclusion, scan the reasoning trace for any step where a claim was asserted without a source and flag it: "Step N relies on model knowledge — verify with [source type]"
- For multi-part questions, number each reasoning step and draw a visible conclusion before moving to the next step, keeping the trace readable

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Add a system-prompt instruction such as: "For any question requiring more than one reasoning step, produce a numbered chain-of-thought trace before your final answer"
- Log reasoning traces separately from final answers in your storage layer, enabling downstream auditing and fine-tuning on high-quality traces
- Set token budgets that allow for reasoning overhead (typically 1.5–3× a direct-answer budget) so CoT is not truncated mid-chain

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

#### Algorithm

**Input:** Research question Q, branching factor B (number of approaches to generate), evaluation threshold T  
**Output:** Best answer A from the most promising reasoning path

1. Receive Q
2. Generate B distinct high-level approaches: approach₁, approach₂, ..., approachB
   - Each approach should represent a meaningfully different framing, method, or angle
3. For each approachᵢ, evaluate its promise on a score 0–10:
   - Score based on: relevance to Q, expected completeness, feasibility, avoidance of known dead ends
4. Prune: discard any approachᵢ with score < T; retain top candidates (typically top 1–2)
5. For each surviving approach, expand one level deeper: generate sub-paths and re-evaluate
6. Pursue the highest-scoring path to a full answer A
7. If no path yields a satisfactory A, lower T and re-expand from step 3
8. Return A with the path taken (for auditability)

**Stopping condition:** A surviving path produces an answer A that satisfies Q, or all branches have been exhausted.  
**Why each step matters:** Step 2 implements systematic breadth (Section 1.6 — SLR principle); step 3 mirrors source evaluation (Section 1.4); pruning in step 4 controls token cost.

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- Explicitly generate at least three distinct framings of the question before choosing one: "I'll consider three approaches: (A) …, (B) …, (C) …. Evaluating each: A scores 7/10 because …, B scores 9/10 because …. I'll develop B."
- After exploring the winning branch, briefly state why the discarded branches were inferior — this preserves auditability and signals the reasoning was deliberate
- For open-ended questions, use ToT to surface assumptions: each branch can represent a different assumption set

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Implement ToT as a multi-call pipeline: call 1 generates candidate approaches, call 2 scores them, call 3 expands the winner — this enables logging and human review at each stage
- Store scored branch evaluations in your trace log; they are valuable for identifying where models consistently misjudge approach quality
- Set a maximum branch depth (e.g., 2–3 levels) to bound token cost; pair with a token budget check before each expansion step

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

#### Algorithm

**Input:** Research question Q, sample count N (recommended: 3–5)  
**Output:** Most reliable answer A*, confidence signal C

1. Receive Q
2. For i = 1 to N:
   - Generate a distinct CoT reasoning chain Rᵢ (use temperature > 0 to introduce variation)
   - Extract the final answer Aᵢ from Rᵢ
3. Collect all answers: {A₁, A₂, ..., Aₙ}
4. Aggregate by majority vote (or semantic equivalence for non-categorical answers):
   - A* = the answer that appears most frequently (or is most semantically central)
   - C = fraction of chains that agree on A* (e.g., 4/5 = high confidence)
5. If C < 0.5, flag A* as low-confidence and surface the disagreement explicitly
6. Return (A*, C, summary of dissenting chains)

**Stopping condition:** N samples have been generated and aggregated.  
**Why each step matters:** Multiple independent chains reduce the chance that a single reasoning error dominates (cross-validation principle, Section 1.4); step 5 preserves honesty about uncertainty rather than hiding disagreement.

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- Explicitly answer the question three times using different reasoning angles, then state: "Across these three attempts, the consistent answer is X (agreed 3/3)" or flag disagreement: "Two attempts gave X; one gave Y — I'll flag this as uncertain"
- When a question is sensitive or high-stakes, volunteer to apply self-consistency: "This is a question where my answer could vary — let me reason through it in two independent ways to check for consistency"
- Surface the minority answer if it exists: it may indicate a genuine edge case the majority answer glosses over

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Run N parallel inference calls at temperature 0.7–1.0 for the same prompt; aggregate answers programmatically before returning to the user
- Expose the confidence signal C in your API response metadata so downstream applications can trigger human review when C < threshold
- Cache the N reasoning chains; if the user asks a follow-up, the cached chains provide context without regenerating from scratch

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

#### Algorithm

**Input:** Research question Q, available tools T = {search, lookup, calculator, …}  
**Output:** Answer A grounded in retrieved evidence, with full Thought–Action–Observation trace

1. Receive Q
2. Thought₁: Identify what information is needed to begin answering Q; select the appropriate tool tᵢ ∈ T
3. Action₁: Execute tᵢ with a precise query derived from Q → receive Observation₁
4. Thought₂: Interpret Observation₁; determine whether it is sufficient, partial, or irrelevant
   - If sufficient → proceed to step 6
   - If partial or irrelevant → formulate a refined query and go to step 3
5. Repeat steps 3–4 for each remaining information need; accumulate Observations
6. From the full Thought–Action–Observation trace, synthesize final answer A
7. Cite each Observation used in A with its source and retrieval action
8. Return (trace, A)

**Stopping condition:** All information needs identified in step 2 have been resolved by Observations, or a maximum iteration limit is reached (to prevent infinite loops).  
**Why each step matters:** Interleaving thought and action grounds each reasoning step in retrieved evidence (primary source principle, Section 1.2); explicit trace supports auditability (Cornell notes principle, Section 1.5).

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- Explicitly structure responses using labeled Thought / Action / Observation blocks, even when simulating actions: "Thought: I need the publication date of paper X. Action: I'll search my training knowledge for this. Observation: My training data indicates …"
- When a tool result is ambiguous, record this in the Thought step before acting on it — do not silently accept uncertain observations
- Disclose when a required action (e.g., live web search) is unavailable, and state what the response would be if that action were available

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Implement a tool-calling loop: parse the model's Action output, route it to the correct tool handler, inject the Observation back into the context, and re-invoke the model until a final answer is produced
- Set a maximum action count (e.g., 10) to prevent runaway loops; return a partial answer with an "incomplete — iteration limit reached" flag if exceeded
- Log every Thought–Action–Observation triplet with timestamps; this trace is the primary artifact for debugging, auditing, and measuring retrieval quality

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

#### Algorithm

**Input:** Compositional research question Q  
**Output:** Final answer A, supported by a chain of intermediate answers

1. Receive Q
2. Determine whether Q requires follow-up questions: if Q is directly answerable → skip to step 6
3. Generate the minimal set of follow-up questions FQ = {fq₁, fq₂, ..., fqₘ} needed to answer Q
   - Order FQs by dependency: fq₁ must not depend on answers not yet known
4. For i = 1 to m:
   - Answer fqᵢ using available knowledge or tools → store intermediate answer IAᵢ
   - Carry IAᵢ forward as context for fqᵢ₊₁
5. Check: do all IAᵢ together provide sufficient basis to answer Q? If not, generate additional follow-up questions and repeat from step 4
6. Synthesize final answer A from {IA₁, ..., IAₘ}
7. Return (FQ, {IAᵢ}, A)

**Stopping condition:** All dependency questions have been answered and A follows directly from the intermediate answers.  
**Why each step matters:** Explicit dependency ordering (step 3) enforces the principle that complex claims must be built from verified simpler claims — the same logic underlying primary-source tracing (Section 1.7).

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- Before answering a multi-hop question, explicitly ask: "Are follow-up questions needed here? Yes/No" — if yes, list them before answering any
- Answer each follow-up question as a labeled intermediate step: "Follow-up: [question] → Intermediate answer: [answer]" — never combine or skip steps, as skipping defeats the compositionality benefit
- If an intermediate answer is uncertain, mark it and propagate that uncertainty to the final answer rather than silently absorbing it

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Implement Self-Ask as a two-pass pipeline: pass 1 generates the follow-up question list and dependency graph; pass 2 resolves each node in dependency order, optionally routing factual sub-questions to a retrieval tool
- Cache intermediate answers keyed by sub-question text — repeated compositional queries often share sub-questions, enabling significant token savings
- Use the intermediate answer chain as a structured citation trail: each IAᵢ is a verifiable claim that can be logged, audited, or surfaced to users on request

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
- Retrieved documents may be irrelevant, outdated, or adversarially poisoned (see [`safety-and-security.md`](../safety-and-security-guide/safety-and-security.md#attack-class-6-adversarial-retrieval-poisoning)).
- Context window limits constrain how many documents can be included.

**Research evidence:** Lewis et al. (2020) \[17\] introduced RAG as a general approach and demonstrated that RAG models outperformed sequence-to-sequence models trained purely on knowledge-intensive tasks (Natural Questions, TriviaQA, WebQuestions), with more specific and factually accurate answers.

#### Algorithm

**Input:** User query Q, retrieval index I (vector database, BM25 index, or hybrid)  
**Output:** Answer A grounded in retrieved documents D*, with source citations

1. Receive Q
2. Encode Q → query vector qᵥ (or structured keyword query for BM25)
3. Retrieve top-k candidate documents from I: D_candidates = Retrieve(I, qᵥ, k)
4. Evaluate retrieved documents for relevance and quality (apply CRAAP / SIFT criteria, Section 1.4):
   - Discard documents below relevance threshold
   - Flag documents from low-authority sources
5. Assemble prompt P = [System instructions] + [Filtered D*] + [Q]
   - If |P| exceeds context window limit → apply chunking or progressive compression (Section 4.4)
6. Generate answer A from P using the LLM
7. For each claim in A, cite the specific document in D* that supports it
8. Return (A, citations to D*)

**Stopping condition:** A is generated and all major claims are attributable to a document in D*.  
**Why each step matters:** Step 4 applies source evaluation before the LLM sees the content (preventing garbage-in/garbage-out); step 7 implements citation integrity (Section 1.7); step 5 manages the practical constraint of finite context windows.

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- When given documents (e.g., pasted by a user or injected by a tool), treat them as the retrieval result: explicitly ground each answer claim in a specific passage and quote or cite it, rather than blending it invisibly with model knowledge
- Distinguish clearly between "according to the provided document" and "from my training knowledge" — this preserves the epistemic transparency that RAG is designed to provide
- If retrieved content contradicts model knowledge, surface the conflict rather than silently resolving it: "The document says X; my training knowledge suggests Y — the document should be treated as more current/authoritative for this fact"

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Build a hybrid retrieval index (dense vector + BM25 sparse) with a re-ranking step; the two methods have complementary failure modes and together retrieve more relevant documents
- Implement a retrieval quality gate: before passing documents to the LLM, score them for relevance (e.g., cross-encoder score > threshold) and drop those below it rather than padding context with low-quality material
- Log query-document pairs with user feedback signals (thumbs up/down, corrections); use these logs to fine-tune the retrieval model and identify systematic retrieval failures

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

#### Algorithm

**Input:** Draft answer D₀, quality criteria C (e.g., accuracy, completeness, logical consistency, citation integrity)  
**Output:** Refined answer Dₙ that satisfies C, with critique log

1. Receive D₀
2. Critique D₀ against each criterion in C:
   - For each criterion cᵢ: does D₀ satisfy cᵢ? If not, describe the specific failure
   - Collect all failures as critique report CR₁
3. If CR₁ is empty (all criteria satisfied) → return D₀ as final answer
4. Refine: generate D₁ by addressing all issues in CR₁ — do not introduce new issues
5. Repeat steps 2–4 for Dₙ (incrementing n) until CR is empty or a maximum iteration count is reached
6. If max iterations reached without satisfying all criteria, return Dₙ with unresolved critiques explicitly noted
7. Return (Dₙ, critique log {CR₁, CR₂, …})

**Stopping condition:** All quality criteria in C are satisfied, or maximum iteration limit is reached.  
**Why each step matters:** Step 2 mirrors peer review and the CRAAP evaluation principle (Section 1.4); the critique log in step 7 is an audit trail analogous to revision history in academic publishing; the explicit stopping condition prevents infinite refinement loops.

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- After producing any substantive answer, explicitly run a self-critique pass: "Let me review this answer: (1) Are all claims supported? (2) Are there gaps? (3) Are there logical errors?" — then state whether a revision is needed and produce it
- Use an explicit quality checklist rather than a vague "review" instruction; specific criteria (accuracy, completeness, neutrality, citation quality) produce more actionable critiques than open-ended self-evaluation
- Limit refinement to two passes in real-time contexts to manage latency; if the answer still has issues after two passes, flag the remaining gaps rather than continuing silently

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Implement critique and refinement as separate sequential LLM calls: call 1 generates D₀, call 2 critiques it against a structured rubric, call 3 produces D₁ — separating the roles reduces mode collapse (where the model praises its own output)
- Consider using a second, independent model (or a fine-tuned critic model) for the critique step; same-model self-critique has a known bias toward over-rating its own output
- Store the full (D₀, CR₁, D₁, …) chain in your logging layer; this data is highly valuable for preference learning and reward model training

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

#### Algorithm

**Input:** Complex research question Q  
**Output:** Final answer A, built from a sequence of progressively harder sub-answers

1. Receive Q
2. **Decomposition stage:** Generate ordered sub-question sequence SQ = [sq₁, sq₂, ..., sqₖ] where:
   - sq₁ is the simplest, most foundational question needed to begin reasoning about Q
   - sqₖ is the most complex sub-question, directly enabling the final answer
   - Each sqᵢ is simpler than sqᵢ₊₁ and its answer is a prerequisite for sqᵢ₊₁
3. **Sequential solving stage:** For i = 1 to k:
   - Solve sqᵢ using: (a) direct model knowledge, or (b) previously accumulated answers {SA₁, …, SAᵢ₋₁}
   - Store answer SAᵢ
   - Pass SAᵢ as explicit context into the prompt for sqᵢ₊₁
4. Synthesize final answer A from {SA₁, …, SAₖ}, with explicit references to which sub-answers it builds on
5. Verify: does A fully address Q? If not, identify the gap and insert a new sub-question at the appropriate position, then repeat from step 3 for that sub-question onward
6. Return (SQ, {SAᵢ}, A)

**Stopping condition:** All sub-questions have been answered and A fully addresses Q.  
**Why each step matters:** The deliberate simple-to-complex ordering (step 2) ensures that harder reasoning always has a verified foundation — this mirrors the scaffolding principle in systematic reviews (Section 1.6) and prevents the error-compounding that occurs when complex questions are tackled without grounding simpler ones first.

#### Dual Implementation

🤖 **AI Instance (Real-Time)** — what an AI chatbot or agent can do immediately, without infrastructure changes:
- For any question that feels complex, begin by explicitly stating the decomposition: "To answer this, I need to first answer these simpler questions in order: (1) …, (2) …, (3) …" — then solve them sequentially, feeding each answer into the next
- When solving each sub-question, reference the previous answer explicitly: "Given that [SA₁], the answer to [sq₂] is …" — this makes the dependency chain visible and auditable
- If a sub-question turns out to be harder than expected, insert an additional intermediate question rather than guessing — maintain the invariant that each step is genuinely simpler than the next

⚙️ **AI Operator / Developer** — infrastructure-level implementation for systems and services:
- Implement least-to-most as a dynamic pipeline: stage 1 produces the ordered sub-question list (store it); stage 2 iterates through the list, injecting accumulated answers as rolling context in each call
- Use the sub-question list from stage 1 as a progress tracker — if the pipeline is interrupted, it can resume from the last completed sub-question without restarting from scratch
- Measure sub-question difficulty empirically (e.g., by model confidence or answer length variance across runs) and use this signal to validate that the ordering is genuinely least-to-most; re-order if the empirical difficulty sequence does not match the intended order

---

## Part 3: Integrating Foundational Principles with AI-Native Techniques

### 3.1 Which Foundational Principles Apply to Each AI Technique

Each AI technique in Part 2 is an implementation of one or more foundational principles from Part 1. This table makes the connection explicit so that AI systems can select the right technique by reasoning from the underlying research principle they need to apply.

| Research goal | Foundational principle (Part 1) | AI technique that implements it (Part 2) |
|---|---|---|
| **Scope and focus a question** | Question formulation (PICO, Bloom's) | Self-Ask (2.5), Least-to-Most (2.8) |
| **Break a complex question into parts** | Decomposition, sub-question structuring | Self-Ask (2.5), Chain-of-Thought (2.1) |
| **Generate and explore multiple angles** | Systematic breadth (SLR, literature survey) | Tree of Thoughts (2.2) |
| **Evaluate source quality** | CRAAP test, SIFT, peer review signals | Critique-and-Refine (2.7), RAG with source attribution (2.6) |
| **Ground answers in verified sources** | Primary source preference, citation integrity | RAG (2.6), ReAct (2.4) |
| **Validate a conclusion against alternatives** | Cross-validation, adversarial checking | Self-Consistency (2.3) |
| **Make reasoning auditable** | Cornell notes, transparent argumentation | Chain-of-Thought (2.1) |
| **Handle complex, real-time, multi-step tasks** | SLR-style iterative refinement | ReAct (2.4) |
| **Improve a draft iteratively** | Revision cycles, peer critique | Critique-and-Refine (2.7) |

### 3.2 An Integrated AI Research Workflow

The following workflow shows how foundational principles and AI-native techniques combine in a complete research session. All steps are performed by the AI system; the foundational principles from Part 1 are the basis for each decision.

```
1. Scope the question using PICO or Bloom's taxonomy (Section 1.1)
   → AI technique: Self-Ask or Least-to-Most to decompose into sub-questions
         │
         ▼
2. Identify source types needed (Section 1.2)
   → AI technique: RAG configuration — primary sources for factual claims,
     secondary for synthesis
         │
         ▼
3. Retrieve relevant sources (Section 1.3 — Boolean/semantic search principles)
   → AI technique: RAG retrieval or ReAct tool use
         │
         ▼
4. Evaluate source quality (Section 1.4 — CRAAP / SIFT)
   → AI technique: Critique-and-Refine applied to each source before use
         │
         ▼
5. Synthesize across sub-questions using Chain-of-Thought (Section 2.1)
   → Compress each sub-answer before the next step (progressive compression,
     Section 4.4)
         │
         ▼
6. Cross-validate key claims with Self-Consistency (Section 2.3)
   → Apply when confidence is needed on factual or contested claims
         │
         ▼
7. Run a final Critique-and-Refine pass on the complete draft (Section 2.7)
   → Check: Are satisfaction criteria met? (Section 4.4)
     If yes → conclude. If no → identify the specific gap and repeat from step 3.
         │
         ▼
8. Cite sources using persistent identifiers (DOI, arXiv ID) (Section 1.7)
   → Apply Citation Source Integrity checks (../safety-and-security-guide/safety-and-security.md)
```

### 3.3 Verifying AI Research Output

AI research output requires specific self-verification steps before delivering a final answer:

1. **Verify all citations.** Every reference should be resolved using a DOI or arXiv ID. Plain LLM generation (without RAG) frequently produces plausible-sounding but nonexistent references. If a citation cannot be verified, disclose this or remove it.

2. **Check for temporal accuracy.** Confirm that the information is not outdated on time-sensitive topics. State your knowledge cutoff explicitly when relevant.

3. **Trace claims to primary sources.** When a secondary or tertiary source is cited, identify the primary source it describes. Secondary sources sometimes misrepresent or oversimplify primary findings.

4. **Apply SIFT principles.** Investigate the origin of any claim before including it. Find better coverage if a single source is uncertain. Trace all claims back to their primary source.

5. **Request reasoning transparency from yourself.** For each key claim, ask: "How did I reach this conclusion?" If the reasoning path cannot be articulated, the claim may be confabulation rather than grounded inference.

6. **Cross-validate important claims.** Check significant claims against at least two independent, authoritative sources.

See also: [`research-quality-guidelines.md`](research-quality-guidelines.md), [`ai-research-processing.md`](ai-research-processing.md), [`user-guidance.md`](user-guidance.md).

---

## Part 4: Contributing New Techniques

> **Why this section exists:** AI research methodology evolves constantly. New AI prompting techniques are published regularly, and practitioners discover practical shortcuts and efficiency patterns that never appear in formal papers. This section makes it easy for anyone (human or AI) to contribute an improvement so that the community can benefit as soon as it is reviewed and merged.

### 4.1 Why Contributions Matter

Every new technique or efficiency improvement added to this document has a multiplicative effect: any AI system that uses this guide as a reference can apply the technique immediately. A single well-described, well-tested method — contributed by one person — can improve the research quality of every AI that reads this document.

Contributions are especially valuable when they:

- Reduce the number of tokens or re-prompting steps needed to achieve the same research quality.
- Improve output accuracy or citation reliability.
- Apply to a new domain (e.g., legal, medical, or scientific research) not yet covered.
- Describe a failure mode of an existing technique and how to avoid it.
- Provide a practical worked example for a technique that currently has only a theoretical description.

### 4.2 How to Propose a New Technique

1. **Open an issue** in this repository titled `[Technique Proposal] <Short name of technique>`.
2. **Fill in the Technique Submission Template** (see Section 4.3 below) in the issue body.
3. A maintainer will review the proposal and assign it a section number (e.g., a new `2.9` for an AI technique, or a new `1.8` for a manual method).
4. **Open a pull request** adding the new subsection in the correct location, following the format below.
5. The PR will be reviewed for accuracy, clarity, and alignment with the rest of the document.

For smaller improvements to existing entries (adding an example, fixing a description, linking a new paper), you can submit a PR directly without opening an issue first.

### 4.3 Technique Submission Template

```markdown
### N.N: <Technique Name>

**Type:** [Manual | AI-Assisted | Hybrid]

**Goal:** <One sentence describing what problem this technique solves.>

**When to use:** <Describe the research scenario where this technique is most useful.>

**How it works:**

<Step-by-step description. Be specific enough that a reader can apply the technique
without referring to any other resource.>

**Efficiency profile:**

| Dimension | Rating (Low / Medium / High) | Notes |
|---|---|---|
| Token cost | | |
| Re-prompting steps | | |
| Time to result | | |
| Output quality | | |

**Example:**

> Input / prompt / question:
> ```
> <Example input>
> ```
>
> Output / result:
> ```
> <Example output or description of what good output looks like>
> ```

**Known limitations or failure modes:**
- <Limitation 1>
- <Limitation 2>

**References:**
- <Citation if this technique is described in a paper or established resource>
```

### 4.4 Efficiency Criteria

Because AI research operates under token budgets and re-prompting limits, **efficiency is a first-class criterion** for techniques listed in this document. When submitting or improving a technique, describe it in terms of the following four dimensions:

| Dimension | What it measures | Why it matters |
|---|---|---|
| **Token cost** | Approximate number of tokens (input + output) consumed per application of the technique | Every token used for methodology is a token not available for content; token-heavy techniques may exceed context limits on long documents |
| **Re-prompting steps** | How many separate AI calls are required to apply the technique end-to-end | More calls increase latency and cost; each call also introduces a potential failure point |
| **Time to result** | Wall-clock time from starting the technique to receiving a usable answer | Matters for interactive use cases where users are waiting |
| **Output quality** | Relative improvement in relevance, accuracy, depth, or citation reliability compared to a plain query | The reason the technique exists — if it doesn't improve quality, it isn't worth the overhead |

**Efficiency guidance for AI systems:**

When choosing between two techniques that produce similar-quality output, prefer the one with lower token cost and fewer re-prompting steps. The following five heuristics help:

- **Front-load the research goal.** State the full research objective at the start of the first prompt, not after several clarifying exchanges. This eliminates re-prompting loops caused by an underspecified goal.
- **Use progressive compression.** After each sub-question is answered, compress the results into a compact summary before asking the next sub-question. This prevents the context window from being consumed by earlier answers.
- **Parallelize independent sub-questions.** When two sub-questions do not depend on each other's answers, ask them in a single prompt to halve the number of re-prompting steps.
- **Declare satisfaction criteria upfront.** Describe what a complete answer looks like at the start of the research session. This allows the AI to self-check and avoid unnecessary additional queries.
- **Stop when criteria are met.** Do not continue researching once all satisfaction criteria are met. Continuing increases token cost without improving quality.

See [`ai-research-processing.md`](ai-research-processing.md) for a detailed treatment of token-efficient research strategies.

### 4.5 Improving Existing Entries

If an existing technique entry (Parts 1–3) needs improvement, the following types of changes are welcomed:

| Improvement type | How to contribute |
|---|---|
| **Add a worked example** | Add an "Example" subsection in the same format as Section 4.3's template. Include real or realistic input/output pairs. |
| **Add an efficiency profile** | Add the efficiency table from Section 4.3's template to any existing technique that lacks one. |
| **Document a failure mode** | Add a "Known limitations" or "When this technique fails" note to an existing technique. |
| **Link a new paper** | Add the citation to the technique section and to the References list at the bottom of the document. |
| **Correct a description** | Submit a PR with the correction and a brief note in the PR description explaining what was wrong and why the correction is accurate. |

All improvements should preserve the existing heading anchor (e.g., `#21-chain-of-thought-prompting`) so that external links remain valid.

See also: [`contributor-guide.md`](../contributor-guide.md), [`ai-research-processing.md`](ai-research-processing.md).

---

### 4.6 Quality Assurance and Cost Control During Fast Research

> **Summary:** Speed and quality are often treated as opposites, but the techniques in this guide are designed so that following the methodology *is* the fast, cost-efficient path. This section explains the mechanisms that enable this, and provides a decision framework for choosing the right trade-off for each situation.

#### Why Following the Methodology Saves Time and Cost

Counter-intuitively, skipping research methodology steps usually *increases* total cost, because:

- **Poorly scoped questions generate off-target answers**, requiring additional re-prompting rounds that together consume more tokens than a well-scoped first prompt would have.
- **Unverified sources cause downstream errors** that are expensive to detect and correct later.
- **Hallucinated citations require manual checking**, which is slower than using RAG or source-verification techniques upfront.
- **Unfocused research loops** (no satisfaction criteria) continue past the point where the research goal is met, wasting both time and tokens.

The techniques in Parts 1–3 are designed specifically to eliminate these failure modes at the cheapest possible point — before they occur.

#### The Quality-Speed-Cost Triangle

Every research task sits somewhere in this trade-off space:

| Constraint | What it means | When it applies |
|---|---|---|
| **Quality-first** | Maximize accuracy, depth, and citation reliability; accept higher token/time cost | High-stakes decisions: medical, legal, financial, safety-critical |
| **Speed-first** | Minimize time-to-answer; accept lower depth; verify key facts manually afterward | Exploratory queries, live conversation, quick summaries |
| **Cost-first** | Minimize token usage and re-prompting steps; accept a narrower scope | High-volume automated pipelines, large document batches |

Most research tasks are **speed-and-quality balanced**: you want a good answer without spending unnecessary tokens. The techniques in this guide are tuned for this middle path.

#### Mechanisms That Ensure Quality Under Speed Pressure

The following built-in mechanisms in this guide's methodology maintain quality even when time and token budgets are tight:

**1. Front-loaded goal declaration (Section 4.4, heuristic: "Front-load the research goal")**  
Stating the full research goal at the start of the first prompt eliminates clarifying exchanges that would otherwise add multiple re-prompting rounds. Quality is maintained because the model has the complete goal context from the first token.

**2. Satisfaction criteria upfront (Section 4.4, heuristic: "Declare satisfaction criteria upfront")**  
Declaring what "done" looks like before starting research allows the AI to self-check and stop exactly when quality criteria are met — neither early (incomplete) nor late (wasteful).

**3. Structured sub-question progression (Section 2.5, Self-Ask)**  
Breaking the main question into sub-questions and solving them in order prevents the AI from going off-topic. Each sub-question is narrow enough to be answered accurately in few tokens.

**4. Progressive compression (Section 4.4, heuristic: "Use progressive compression")**  
Compressing each intermediate result into a compact summary before the next step prevents the context window from filling with verbose earlier answers that crowd out the current question. This maintains quality (context available to the model stays relevant) while reducing token usage.

**5. Source quality gatekeeping (Section 1.4, CRAAP and SIFT)**  
Evaluating source quality before synthesis prevents low-quality sources from degrading the final answer. A few tokens spent on source evaluation save many tokens of correction later.

**6. RAG for factual precision (Section 2.6)**  
Retrieval-Augmented Generation grounds answers in verified retrieved documents rather than model weights alone. This reduces hallucination at low additional cost, since retrieval replaces some generation tokens with more accurate retrieved text.

**7. Self-critique gating (Section 2.7)**  
Running a single critique pass on a draft response before delivering it catches the most common errors cheaply, without requiring a full second research pass.

#### Fast Research Decision Framework

Use this framework to choose the right technique set for a given research task:

```
Is the question well-defined?
├── No → Apply Section 1.1 (PICO / Bloom) to sharpen the question first
│         (Saves: 2–5 re-prompting rounds)
└── Yes
    │
    Is real-time / retrieved information required?
    ├── Yes → Use RAG (Section 2.6) or ReAct (Section 2.4)
    │         (Saves: hallucination correction overhead)
    └── No
        │
        Is the question multi-part or complex?
        ├── Yes → Use Self-Ask (Section 2.5) or Least-to-Most (Section 2.8)
        │         (Saves: context drift, irrelevant detours)
        └── No
            │
            Is high confidence required?
            ├── Yes → Use Self-Consistency (Section 2.3) + source verification
            │         (Saves: downstream error correction)
            └── No → Use Chain-of-Thought (Section 2.1)
                      (Lowest token cost for quality single-answer tasks)
```

#### Cost-per-Quality Comparison of Key Techniques

The following table summarizes the approximate cost-quality profile of each AI technique in this guide. "Cost" refers to relative token+re-prompting overhead; "Quality ceiling" refers to the maximum answer quality achievable with the technique.

| Technique | Token cost | Re-prompting steps | Quality ceiling | Best for |
|---|---|---|---|---|
| Plain query (no technique) | Very low | 1 | Low–medium | Trivial factual lookups |
| Chain-of-Thought (2.1) | Low | 1 | Medium–high | Reasoning-heavy single questions |
| Self-Consistency (2.3) | Medium | 3–5 | High | Questions with right/wrong answers |
| Self-Ask (2.5) | Low–medium | 2–4 | High | Multi-part questions |
| Least-to-Most (2.8) | Low–medium | 2–4 | High | Hierarchically complex questions |
| RAG (2.6) | Medium | 1–2 | Very high | Factual/cited claims |
| ReAct (2.4) | Medium–high | 3–6 | Very high | Research requiring external actions |
| Critique-and-Refine (2.7) | Medium | 2 | High | Draft improvement |
| Tree of Thoughts (2.2) | High | 3–8 | Very high | Open-ended exploration, planning |

**Rule of thumb:** For most research tasks, Chain-of-Thought + Self-Ask + a final Critique pass provides the best quality-per-token ratio. Upgrade to RAG or ReAct only when retrieved, up-to-date information is necessary.

#### Avoiding Common Cost-Quality Trade-off Mistakes

| Mistake | What goes wrong | Cheaper fix |
|---|---|---|
| Asking a broad question then narrowing | 3–5 re-prompting rounds to converge on scope | Apply PICO/Bloom before the first prompt |
| Using Tree of Thoughts for every question | 3–8× token cost with marginal gain on simple questions | Reserve ToT for genuinely open-ended exploration |
| Requesting a long answer and then summarizing | Pays for generation of content that is immediately discarded | Ask for the summary directly; specify length upfront |
| Re-running full research after a small error | Repeats all token cost to fix a narrow issue | Use Critique-and-Refine (2.7) to patch the specific error |
| Citing without verifying | Requires manual verification session later | Use RAG or ask for verifiable identifiers (DOIs, arXiv IDs) in the original prompt |

See also: [`ai-research-processing.md` — "Efficient Research Within Token and Re-Prompting Limits"](ai-research-processing.md#efficient-research-within-token-and-re-prompting-limits) for the full token-efficiency strategy treatment.

---

## Part 5: Step-by-Step Research Guide with Key Questions

> **What this part is for:** This section provides a practical, step-by-step research guide that an AI system can follow for any research task. At each step, we provide specific questions (What? Why? How? When? Which? Where?) that guide decision-making. We also explain *why* following each step makes research faster, more efficient, more effective, and produces higher-quality results that satisfy the original ask.

### 5.1 Overview: The Research Effectiveness Framework

Every research task should produce outputs that meet four key criteria:

| Criterion | Definition | How This Guide Achieves It |
|-----------|------------|---------------------------|
| **Effective** | Output fully satisfies the original ask | Clear goal definition, satisfaction criteria, synthesis verification |
| **Efficient** | Minimum tokens/compute per quality unit | Progressive compression, parallel sub-questions, early stopping |
| **Fast** | Minimum wall-clock time and re-prompting | Front-loaded goals, structured decomposition, technique selection |
| **Quality** | Accurate, well-grounded, properly cited | Source evaluation, RAG verification, self-critique loops |

---

### 5.2 Step 1: Understand the Research Goal

**Purpose:** Before any research begins, clearly understand what the user wants. Ambiguity at this stage multiplies into wasted effort downstream.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **WHAT** | What specific outcome does the user need? | Defines success criteria |
| **WHAT** | What form should the output take? (summary, analysis, comparison, recommendation) | Shapes the research approach |
| **WHY** | Why does the user need this information? | Reveals unstated requirements and appropriate depth |
| **WHO** | Who is the intended audience? | Determines technical level and terminology |
| **WHEN** | Is there a time constraint or deadline? | Guides speed-quality trade-off |
| **WHICH** | Which aspects are most important vs. nice-to-have? | Enables prioritization if time is limited |
| **WHERE** | Where will this output be used? (decision, report, code, conversation) | Shapes format and citation requirements |

#### Why This Step Makes Research Effective and Fast

- **Avoids re-prompting loops:** A well-understood goal eliminates 2–5 clarification exchanges that would otherwise waste tokens and time.
- **Enables satisfaction criteria:** Clear goals allow you to know when you're done, preventing over-research.
- **Focuses sub-questions:** All subsequent decomposition derives from this understanding.

#### Practical Application

```
Goal Analysis Template:
─────────────────────────
Original ask: [User's question]
Core need: [What the user actually wants to achieve]
Output format: [Summary / Analysis / Comparison / Recommendation / Code / etc.]
Audience: [Technical level and context]
Success looks like: [Specific criteria for a satisfactory answer]
Key constraints: [Time, scope, depth requirements]
```

---

### 5.3 Step 2: Decompose into Sub-Questions

**Purpose:** Break the main question into smaller, answerable components. This is the single most impactful efficiency technique.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **WHAT** | What are the component parts of this question? | Identifies research threads |
| **WHAT** | What must I know before I can answer the main question? | Reveals dependencies |
| **WHICH** | Which sub-questions are independent (can be answered in parallel)? | Enables parallelization |
| **WHICH** | Which sub-questions depend on answers to others? | Establishes ordering |
| **HOW** | How do these sub-answers combine to form the final answer? | Plans synthesis step |
| **WHEN** | When can I stop decomposing? (sub-questions are directly answerable) | Prevents over-decomposition |

#### Why This Step Makes Research Efficient and Quality-Focused

- **Prevents context drift:** Each sub-question is focused enough to answer accurately in limited tokens.
- **Enables quality per sub-answer:** Smaller questions are easier to verify.
- **Supports progressive compression:** Answer each sub-question, compress, then proceed.
- **Enables parallelization:** Independent sub-questions can be answered simultaneously.

#### Practical Application

```
Decomposition Template:
───────────────────────
Main question: [User's research question]

Sub-questions (ordered by dependency):
1. [Sub-question 1] — Independent / Depends on: []
2. [Sub-question 2] — Independent / Depends on: []
3. [Sub-question 3] — Depends on: [1, 2]
4. [Sub-question 4] — Depends on: [3]

Synthesis plan: Combine answers to [1,2,3,4] into [output format]
```

---

### 5.4 Step 3: Identify and Retrieve Sources

**Purpose:** Gather information from the right places to ground your answers in evidence.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **WHAT** | What type of source is needed? (primary, secondary, tertiary) | Guides search strategy |
| **WHERE** | Where should I look? (model knowledge, RAG retrieval, web search, databases) | Selects information channels |
| **WHICH** | Which databases or retrieval systems are most relevant? | Optimizes search efficiency |
| **WHEN** | How current does the information need to be? | Determines if retrieval is necessary |
| **HOW** | How should I construct the search query? | Improves precision and recall |
| **HOW MANY** | How many sources are sufficient? | Prevents over-retrieval |

#### Source Selection Decision Tree

```
Does the question require:
├── Current/real-time information?
│   └── YES → Use RAG or ReAct with retrieval
├── Verified factual claims with citations?
│   └── YES → Use RAG with source attribution
├── Domain-specific expertise?
│   └── YES → Search specialized databases (PubMed, IEEE, arXiv, etc.)
└── General synthesis from training knowledge?
    └── Model knowledge sufficient (but verify key claims)
```

#### Why This Step Makes Research Grounded and Efficient

- **Right source for the question:** Using RAG for factual claims prevents hallucination.
- **Avoids over-retrieval:** Knowing when model knowledge suffices saves retrieval overhead.
- **Enables citation:** Retrieved sources can be cited with persistent identifiers.

---

### 5.5 Step 4: Evaluate Source Quality

**Purpose:** Not all sources are equally reliable. Evaluate before synthesizing.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **WHAT** | What is the source type? (peer-reviewed, preprint, blog, commercial) | Signals reliability level |
| **WHO** | Who created this content? What are their credentials? | Authority assessment |
| **WHEN** | When was this published? Is it current enough? | Currency check |
| **WHY** | Why was this content created? (inform, persuade, sell) | Bias detection |
| **HOW** | How well does this source support the specific claim? | Relevance verification |
| **WHERE** | Where does this source get its information? Can I trace to primary? | Source chain verification |

#### Quick Quality Check (CRAAP Adaptation for AI)

For each source, score 1–5 on:

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Currency** | 1-5 | Is the information timely? |
| **Relevance** | 1-5 | Does it directly address the sub-question? |
| **Authority** | 1-5 | Is the author/publisher credible? |
| **Accuracy** | 1-5 | Is it supported by evidence? |
| **Purpose** | 1-5 | Is it objective, or is there bias? |

**Use sources scoring ≥15 total.** For lower scores, either find better sources or explicitly note the limitation.

#### Why This Step Prevents Errors and Saves Correction Time

- **Catches bad sources early:** Removing unreliable sources before synthesis is cheaper than correcting errors after.
- **Enables confident synthesis:** High-quality sources support stronger conclusions.
- **Supports transparency:** Quality assessment can be shown to users.

---

### 5.6 Step 5: Synthesize Answers

**Purpose:** Combine information from multiple sources and sub-questions into a coherent answer.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **HOW** | How do the sub-answers connect to form a complete answer? | Guides integration |
| **WHAT** | What are the points of agreement across sources? | Identifies consensus |
| **WHAT** | What are the points of disagreement or uncertainty? | Flags areas needing nuance |
| **WHICH** | Which evidence most directly supports each claim? | Ensures grounding |
| **HOW** | How confident am I in each part of the answer? | Enables uncertainty disclosure |
| **WHAT** | What is missing that I couldn't find? | Acknowledges gaps |

#### Synthesis Process

```
For each sub-question answer:
1. Compress to key findings (progressive compression)
2. Note confidence level (high/medium/low)
3. Note source(s) supporting the finding

Then integrate:
4. Connect sub-answers following the decomposition plan
5. Resolve conflicts (prefer higher-quality sources)
6. Flag remaining uncertainties
7. Structure per the output format specified in Step 1
```

#### Why This Step Produces Quality, Goal-Satisfying Outputs

- **Structured integration:** Following the decomposition plan ensures completeness.
- **Compression prevents context overflow:** Each sub-answer is compacted before synthesis.
- **Uncertainty handling:** Acknowledging limits increases trustworthiness.

---

### 5.7 Step 6: Verify and Cite

**Purpose:** Check that claims are accurate and properly attributed.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **WHAT** | What are the key factual claims in my answer? | Identifies verification targets |
| **HOW** | How can each claim be verified? (DOI, arXiv ID, reproducible lookup) | Enables citation |
| **WHERE** | Where did each claim originate? (my synthesis vs. specific source) | Tracks attribution |
| **WHICH** | Which claims need explicit citation? | Guides citation placement |
| **HOW** | How confident am I that each citation actually supports the claim? | Prevents citation-claim mismatch |

#### Verification Checklist

- [ ] Every factual claim can be traced to a source or is flagged as synthesis/inference
- [ ] Citations include persistent identifiers (DOI, arXiv ID, URL with archive date)
- [ ] No citation supports a claim stronger than the source actually makes
- [ ] Time-sensitive information has a date or currency note
- [ ] Uncertainties are disclosed, not hidden

#### Why This Step Ensures Accuracy and Trust

- **Prevents hallucinated citations:** Verification catches plausible-sounding but nonexistent references.
- **Enables user verification:** Persistent identifiers let users check sources.
- **Maintains intellectual honesty:** Proper attribution respects source authors.

---

### 5.8 Step 7: Self-Evaluate Against Satisfaction Criteria

**Purpose:** Before delivering, confirm the output meets the original goal.

#### Key Questions to Ask

| Question Type | Question | Why It Matters |
|---------------|----------|----------------|
| **WHAT** | What were the original satisfaction criteria from Step 1? | Anchors evaluation |
| **HOW** | How well does my output address each criterion? | Gap identification |
| **WHAT** | What is still missing or incomplete? | Reveals needed fixes |
| **HOW** | How would a critical reader challenge this answer? | Anticipates objections |
| **WHICH** | Which parts are strongest/weakest? | Guides revision priority |
| **WHEN** | When have I done enough? | Prevents over-research |

#### Self-Evaluation Checklist

| Criterion | Met? | Evidence |
|-----------|------|----------|
| Addresses the original ask | ☐ | |
| Correct output format | ☐ | |
| Appropriate depth for audience | ☐ | |
| Key claims are supported | ☐ | |
| Uncertainties disclosed | ☐ | |
| Citations verifiable | ☐ | |

If any criterion is not met, return to the relevant step (decomposition, retrieval, synthesis) and iterate.

#### Why This Step Ensures Effectiveness and Prevents Over-Research

- **Confirms goal satisfaction:** The output demonstrably answers what was asked.
- **Enables early stopping:** Once criteria are met, stop — no wasted tokens.
- **Catches gaps before delivery:** Easier to fix now than after the user points them out.

---

### 5.9 Summary: The Complete Research Flow

```
┌─────────────────────────────────────────────────────────────────────┐
│                    RESEARCH EFFECTIVENESS FLOW                      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. UNDERSTAND GOAL ───────────────────────────────────────────────│
│     • What does the user need? Why? For whom?                      │
│     • Define satisfaction criteria                                  │
│     ↓ (Saves: 2–5 re-prompting rounds)                             │
│                                                                     │
│  2. DECOMPOSE ─────────────────────────────────────────────────────│
│     • What are the sub-questions?                                  │
│     • Which are independent? Which depend on others?               │
│     ↓ (Saves: context drift, enables parallelization)              │
│                                                                     │
│  3. RETRIEVE SOURCES ──────────────────────────────────────────────│
│     • Where should I look? What source type?                       │
│     • Use RAG for factual/current claims                           │
│     ↓ (Saves: hallucination correction overhead)                   │
│                                                                     │
│  4. EVALUATE SOURCES ──────────────────────────────────────────────│
│     • Who created this? Is it reliable?                            │
│     • Score using CRAAP or equivalent                              │
│     ↓ (Saves: downstream error correction)                         │
│                                                                     │
│  5. SYNTHESIZE ────────────────────────────────────────────────────│
│     • How do sub-answers connect?                                  │
│     • Use progressive compression                                  │
│     ↓ (Saves: context overflow, produces structured output)        │
│                                                                     │
│  6. VERIFY & CITE ─────────────────────────────────────────────────│
│     • Can each claim be traced to a source?                        │
│     • Add persistent identifiers                                   │
│     ↓ (Saves: trust issues, enables user verification)             │
│                                                                     │
│  7. SELF-EVALUATE ─────────────────────────────────────────────────│
│     • Does output meet satisfaction criteria?                      │
│     • If yes → deliver. If no → iterate.                           │
│     ↓ (Saves: unnecessary over-research)                           │
│                                                                     │
│  ═══════════════════════════════════════════════════════════════   │
│  RESULT: Effective, efficient, fast, quality research output       │
└─────────────────────────────────────────────────────────────────────┘
```

---

### 5.10 Worked Example: Applying the Framework

**Original ask:** "Compare the energy efficiency of transformer models vs. state-space models for language modeling. Which is more practical for deployment?"

#### Step 1: Understand Goal

| Aspect | Analysis |
|--------|----------|
| Core need | Decision support for model architecture selection |
| Output format | Comparison with recommendation |
| Audience | Technical (ML engineers/researchers) |
| Success criteria | Covers both architectures, cites benchmarks, gives actionable recommendation |

#### Step 2: Decompose

1. What are transformer models and their energy characteristics? (Independent)
2. What are state-space models and their energy characteristics? (Independent)
3. What benchmarks compare their energy efficiency? (Independent)
4. What are the practical deployment considerations beyond raw efficiency? (Depends on 1, 2)
5. Which is more practical for deployment, given the evidence? (Depends on 1–4)

#### Steps 3–4: Retrieve and Evaluate

- Use RAG to retrieve recent papers on Mamba, S4, and transformer efficiency
- Prioritize peer-reviewed benchmarks and major lab publications
- Score sources: arXiv preprints with extensive experiments (score 4–5), blog posts without data (score 2)

#### Step 5: Synthesize

- Compile efficiency metrics from retrieved papers
- Note where transformers excel (hardware optimization, ecosystem maturity)
- Note where SSMs excel (linear scaling with sequence length)
- Structure as: Background → Comparison table → Deployment considerations → Recommendation

#### Step 6: Verify

- Confirm cited papers exist with correct arXiv IDs
- Verify benchmark numbers match source claims

#### Step 7: Self-Evaluate

| Criterion | Met? |
|-----------|------|
| Compares both architectures | ✓ |
| Cites benchmarks | ✓ |
| Addresses deployment practicality | ✓ |
| Gives recommendation | ✓ |

**Output:** [Deliver synthesized comparison with recommendation]

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
