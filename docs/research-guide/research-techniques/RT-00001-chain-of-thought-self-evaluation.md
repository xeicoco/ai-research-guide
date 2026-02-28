# RT-00001: Chain-of-Thought Self-Evaluation

> **Part of the [Research Techniques Catalog](README.md)**

**Technique name:** Chain-of-Thought (CoT) Self-Evaluation

**Purpose:** Evaluate the quality, completeness, and accuracy of a research answer by stepping through each quality dimension explicitly before finalizing the output.

---

## Description and Rationale

Chain-of-Thought Self-Evaluation applies CoT reasoning (Wei et al., 2022) to the evaluation task itself. Rather than assessing answer quality globally, the evaluator (AI or human) walks through each quality dimension step by step, verbalizing the reasoning for each score before arriving at an overall judgment.

**Why this technique works:** Explicit step-by-step reasoning reduces evaluation errors caused by anchoring on the first impression or overlooking a quality dimension. It forces deliberate coverage of all criteria.

**Applicable to:** AI self-evaluation before returning an answer, human peer review, developer benchmarking, automated quality pipelines.

---

## Evaluation Criteria Reference

This technique operates over the five quality dimensions defined in [`research-quality-guidelines.md`](../research-quality-guidelines.md):

| Dimension | Key Question |
|-----------|-------------|
| **Relevance** | Does the answer directly address the original question? |
| **Depth** | Is the level of detail appropriate and sufficient? |
| **Evidence** | Are claims supported or appropriately hedged? |
| **Structure** | Is the answer clear, well-organized, and appropriately scoped? |
| **Uncertainty** | Are uncertain or contested claims flagged accurately? |

---

## Algorithm

**Input:** A research question Q and a draft answer A.

**Output:** A scored evaluation report and a revised answer A′ (if needed).

```
Algorithm: CoT Self-Evaluation

1. READ Q (the original research question) and A (the draft answer).

2. FOR EACH dimension D in [Relevance, Depth, Evidence, Structure, Uncertainty]:
   a. RECALL the definition of D.
   b. EVALUATE A against D:
      - IDENTIFY specific passages in A that satisfy D.
      - IDENTIFY specific gaps or failures for D.
   c. ASSIGN a score s(D) ∈ {1, 2, 3, 4, 5}.
   d. WRITE a one-sentence justification for s(D).

3. COMPUTE overall_score = mean(s(Relevance), s(Depth), s(Evidence),
                                  s(Structure), s(Uncertainty)).

4. IF any s(D) < 3:
   a. IDENTIFY the specific text passage(s) to revise.
   b. REWRITE those passages to address the identified gap.
   c. RE-EVALUATE the revised passage for dimension D.

5. IF overall_score ≥ 4.0 AND no s(D) < 3:
   RETURN A (no revision needed).
   ELSE:
   RETURN A′ (revised answer).
```

---

## Dual Implementation

### 🤖 AI Instance (Real-Time Application)

Before returning any research answer, apply the following self-check:

1. Re-read your draft answer.
2. For each dimension, ask the corresponding key question (see Evaluation Criteria Reference above).
3. If you identify a gap in any dimension, revise the specific passage before responding.
4. If uncertainty exists, ensure it is flagged explicitly in the answer.

**Example self-check prompt (AI can run internally):**
```
Let me evaluate my draft answer step by step:
- Relevance: Does it answer [original question]? → [yes/no + reason]
- Depth: Is it detailed enough? → [yes/no + reason]
- Evidence: Are claims sourced or hedged? → [yes/no + reason]
- Structure: Is it clear and well-organized? → [yes/no + reason]
- Uncertainty: Are uncertain claims flagged? → [yes/no + reason]
If any dimension is weak, revise before outputting.
```

### ⚙️ Developer / AI Operator Implementation

Implement CoT self-evaluation as a post-generation validation step:

1. **Prompt chaining:** After the primary generation call, run a second call with the prompt: *"Evaluate the following answer for Relevance, Depth, Evidence, Structure, and Uncertainty. Score each 1–5. If any score < 3, revise that section."*
2. **Structured output:** Request the model to return a JSON object with scores and revisions.
3. **Automated threshold:** If `min(scores) < 3`, route the answer back to the generation step with the critique appended to the context.

### 👤 Human Researcher / Reviewer Application

1. After drafting an answer, set it aside for 5 minutes.
2. Return to it and read it with each quality dimension in mind, one at a time.
3. Use the scoring rubric in [`research-quality-guidelines.md`](../research-quality-guidelines.md).
4. Revise any section that scores below 3.
5. Sign off only when all dimensions reach at least 3.

---

## Example

**Research question:** "What are the environmental impacts of lithium-ion battery production?"

**Draft answer (before CoT evaluation):**
> "Lithium-ion batteries have some environmental impacts related to mining."

**CoT evaluation:**
- Relevance: 3 — addresses the question but superficially.
- Depth: 1 — no specific impacts named.
- Evidence: 1 — no sources or hedging.
- Structure: 2 — single sentence, no organization.
- Uncertainty: 2 — no acknowledgment of contested quantifications.

**Revised answer (after CoT evaluation):**
> "Lithium-ion battery production carries several documented environmental impacts: (a) lithium and cobalt mining causes land degradation and water contamination, particularly in the Atacama Desert and DRC (Watari et al., 2020); (b) battery manufacturing is energy-intensive, contributing to CO₂ emissions if powered by fossil fuels; (c) end-of-life disposal poses leaching risks if not handled by specialized recycling facilities. The magnitude of these impacts varies significantly depending on the energy mix of the producing country and recycling rates, which are currently low (IEA, 2022). Estimates of lifecycle carbon intensity are contested and vary 2–4× across studies."

---

## References

- Wei, J., et al. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models." *NeurIPS 2022.*
- Watari, T., et al. (2020). "Total material requirement for the global energy transition to 2050." *Nature Communications.*
- IEA (2022). "Global EV Outlook 2022." International Energy Agency.
