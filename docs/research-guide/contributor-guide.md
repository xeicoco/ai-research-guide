# Research Quality Guide — Contributor Guide

> **Section summary:** This document explains how to contribute to the **AI Research Quality Guide** (`docs/research-guide/`). It covers what to contribute, which files to target, format requirements, quality checklists, and the contribution workflow.

---

## Table of Contents

- [What to Contribute](#what-to-contribute)
- [Quick Reference: Target Files](#quick-reference-target-files)
- [Format and Schema Guidance](#format-and-schema-guidance)
- [Avoiding Research Quality Regression](#avoiding-research-quality-regression)
- [Contribution Workflow](#contribution-workflow)
  - [Manual Workflow](#manual-workflow)
  - [Using @copilot to Assist Your Contribution](#using-copilot-to-assist-your-contribution)
  - [Using a Third-Party AI Agent to Assist Your Contribution](#using-a-third-party-ai-agent-to-assist-your-contribution)
- [Style Guide](#style-guide)

---

## What to Contribute

Contributions that make AI research more **effective, efficient, fast, and cost-effective** are especially welcome. Examples include:

- **New AI research techniques** — Chain-of-Thought variants, ReAct, RAG, Self-Ask extensions, or other prompting strategies documented in the academic or practitioner literature.
- **Evaluation techniques** — New algorithmic techniques (RT-NNNNN format) that allow AI systems or developers to verify research quality.
- **Quality guidelines** — New quality dimensions, improvements to the five existing quality dimensions, or new failure-mode entries.
- **Research processing guidance** — Improved strategies for relevance decisions, sub-question formulation, token-efficient research, or cost control.
- **Factual corrections and depth improvements** — Corrections to errors, updated citations, or expanded explanations of existing content.

---

## Quick Reference: Target Files

| What you want to contribute | Target file |
|-----------------------------|-------------|
| New AI research technique (CoT, RAG, Self-Ask variants, etc.) | [`how-to-research.md`](how-to-research.md) — Part 2 |
| Research step-by-step improvement | [`how-to-research.md`](how-to-research.md) — Part 5 |
| Efficiency improvement or cost-saving strategy | [`ai-research-processing.md`](ai-research-processing.md) |
| Quality guideline or quality dimension improvement | [`research-quality-guidelines.md`](research-quality-guidelines.md) |
| New evaluation technique | [`research-techniques/`](research-techniques/) — RT-NNNNN format |
| Failure mode or known limitation | [`research-quality-guidelines.md`](research-quality-guidelines.md) or technique entry |
| Conceptual model improvement | [`conceptual-model.md`](conceptual-model.md) |
| User-facing research guidance | [`user-guidance.md`](user-guidance.md) |

---

## Format and Schema Guidance

### Research Technique Contributions (`how-to-research.md` Part 2)

Each technique entry in Part 2 covers these fields in this order:

1. **Goal** — What research problem does the technique solve?
2. **When to use** — Conditions or contexts where this technique is most appropriate.
3. **How it works** — A clear description of the technique's mechanism.
4. **Efficiency profile** — Token cost estimate, re-prompting steps, time to result (cite a source or label as an estimate).
5. **Example** — A realistic input/output pair illustrating the technique.
6. **Known limitations** — Failure modes and edge cases.
7. **References** — Academic citations in the format used throughout the document.

Follow the heading anchor format already in use (e.g., `## 2.9 New Technique Name`) so external links remain stable.

### Evaluation Technique Contributions (RT-NNNNN format)

Each file in `research-techniques/` uses the standard technique file structure from [`research-techniques/README.md#standard-technique-file-structure`](research-techniques/README.md#standard-technique-file-structure):

1. **RT number and short name** — Assign the next available RT number (e.g., `RT-NNNNN`). Filename: `RT-NNNNN-short-name.md`.
2. **Description and rationale** — What the technique evaluates and why.
3. **Evaluation criteria reference** — Which of the five quality dimensions the technique addresses.
4. **Formal algorithm** — A step-by-step algorithm reproducible by an AI system or a human.
5. **Dual implementation** — Separate guidance for (a) AI systems applying the technique in real-time and (b) developers/humans implementing it as a pipeline step.
6. **Worked example** — A realistic input/output pair demonstrating the algorithm.
7. **References** — Academic citations.

After creating the file, add the technique to the index tables in both [`research-techniques/README.md`](research-techniques/README.md) and [`evaluation-and-test-cases.md`](evaluation-and-test-cases.md).

### Quality Guideline Contributions (`research-quality-guidelines.md`)

Follow the structure of the five existing quality dimensions (Relevance, Depth, Evidence, Structure, Uncertainty). Each dimension entry includes:

- What good looks like.
- What poor looks like.
- Common failure modes and mitigation strategies.

---

## Avoiding Research Quality Regression

Before opening a PR that touches any research quality file, work through this checklist:

- [ ] **Citations are verifiable.** Every academic citation you add (author, year, title, venue, URL) has been independently verified to exist and to accurately describe what the text claims it says. Do not rely on AI-generated citations without checking them.
- [ ] **No new hallucination vectors.** Your contribution does not instruct or encourage AI systems to generate content without source verification, skip uncertainty disclosures, or claim certainty where none exists.
- [ ] **Existing guidelines are preserved.** You have not removed, weakened, or contradicted any of the five quality dimensions (relevance, depth, evidence, structure, uncertainty) from [`research-quality-guidelines.md`](research-quality-guidelines.md) or any step in the integrated AI research workflow in [`how-to-research.md`](how-to-research.md).
- [ ] **Examples are realistic.** Any new worked example demonstrates a real, plausible scenario — not an artificially perfect case that would mislead AI systems about typical performance.
- [ ] **Efficiency claims are justified.** Any efficiency profile (token cost, re-prompting steps, time to result) is either cited from published research or explicitly labelled as an estimate requiring community calibration.
- [ ] **Scope is appropriate.** New techniques or guidelines apply to the AI research use case documented in this guide — not to unrelated AI capabilities that would expand the guide beyond its stated scope.

**During review**, a maintainer will specifically verify:

- That no existing quality heuristic or technique entry has been silently removed or weakened.
- That new techniques are genuinely additive and do not contradict the efficiency criteria in Section 4.4.
- That all failure-mode entries include both the failure description and a concrete prevention strategy.

---

## Contribution Workflow

### Manual Workflow

Use this path when you want full control over every word without AI assistance.

1. **Fork** this repository to your own GitHub account.
2. **Create a branch** for your change:
   ```
   git checkout -b add-cot-variant-technique
   ```
3. **Edit the relevant file(s)** under `docs/research-guide/`, following the [Style Guide](#style-guide) and the [Format and Schema Guidance](#format-and-schema-guidance) above.
4. **Check your changes:**
   - Verify every factual claim has a citation or is well-established common knowledge.
   - Confirm every internal link (`[text](../path/file.md#anchor)`) resolves correctly.
   - Ensure no existing heading anchor has been changed (many external links depend on them).
5. **Open a pull request** with:
   - A clear title (e.g., `Add RT-00007: Adversarial Self-Critique evaluation technique`).
   - A description covering: what you changed, why, which sections are affected, and any sources you relied on.
6. A maintainer will review and may request adjustments before merging.

### Using @copilot to Assist Your Contribution

[GitHub Copilot](https://github.com/features/copilot) can help you draft, improve, and fact-check contributions. Use these workflows:

**Copilot Chat (VS Code or GitHub.com):**

1. Fork and create a branch (steps 1–2 above).
2. Open Copilot Chat (`Ctrl+Shift+I` / `Cmd+Shift+I` in VS Code).
3. Paste the relevant section and describe your request. Examples:
   - "Improve this explanation of Chain-of-Thought prompting for a beginner audience — here is the current text: [paste]"
   - "Add two worked examples to this Self-Ask section with realistic input/output pairs: [paste]"
   - "Review this draft paragraph for factual accuracy and suggest any missing citations: [paste]"
4. Review the suggested output carefully (see checklist below).
5. Apply accepted suggestions to the file in your branch.
6. Open or update your pull request for human maintainer review.

**@copilot in a PR comment (Copilot coding agent):**

1. Fork, create a branch, and open a pull request (draft is fine).
2. Post a PR comment mentioning `@copilot` with your request. Examples:
   - `@copilot improve the explanation of Chain-of-Thought prompting in docs/research-guide/how-to-research.md section 2.1 — make it clearer for a beginner audience`
   - `@copilot add two worked examples to the Self-Ask section with realistic input/output pairs`
3. Copilot will propose changes as a commit to your branch.
4. Review and approve the changes before the PR is merged.

**Review checklist for all Copilot-generated content:**

- Verify every factual claim independently.
- Confirm every citation exists and accurately describes what the text says.
- Confirm the tone and style match the rest of the document.
- Reject any suggestion that introduces unverifiable claims, fabricated citations, or off-topic content.

> **Important:** Copilot suggestions are AI-generated and may contain errors or hallucinations. You are responsible for verifying all content before it is merged.

### Using a Third-Party AI Agent to Assist Your Contribution

You may use any external AI tool (ChatGPT, Claude, Gemini, Perplexity, or any other) to help draft or improve content.

**Recommended workflow:**

1. Read the section you want to improve so you understand what already exists.
2. Prompt the AI agent clearly, including:
   - The current content of the section (copy-paste it).
   - What you want improved or added.
   - The audience and tone.
   - Any specific constraints (e.g., "add a citation to a peer-reviewed paper").

   Example prompt:
   > "I am contributing to an open-source research guide. Here is the current content of section 2.3 on Self-Consistency prompting: [paste content]. Please improve the explanation to be clearer for a non-specialist reader and add an example with realistic input/output. Cite Wang et al. (2022) for the technique."

3. Review the AI output critically — check every citation, verify examples are realistic, confirm style matches the guide.
4. Edit the generated content as needed. AI-generated drafts are starting points, not final text.
5. Fork, branch, and open a PR (manual workflow steps 1–6) with your revised content.
6. **Disclose AI assistance** in the PR description. This is required: include a note such as "This PR was drafted with AI assistance and reviewed for accuracy."

> **Important:** You are responsible for the accuracy and quality of all content you submit. AI-generated content that introduces factual errors, fabricated citations, or off-topic material will be rejected in review.

---

## Style Guide

- **Use Markdown** for all documentation.
- **Use clear headings** (H2 for major sections, H3 for subsections). This helps both humans and AI systems navigate.
- **Use bullet points and numbered lists** to break down complex ideas.
- **Define technical terms** the first time they appear in each document. Avoid unexplained jargon.
- **Keep sections self-contained** so that an AI can quote or summarize a single section without losing context.
- **Use neutral, inclusive language.** Avoid idioms that may not translate well.
- **Cite sources** where possible. If a claim is uncertain, say so explicitly.
- **Do not add unnecessary formatting** (excessive bold, italics, or horizontal rules).
- **File names** should be lowercase and hyphenated (e.g., `research-quality-guidelines.md`).
- **Preserve existing heading anchors.** Many internal links in other files depend on them; do not rename headings without a strong reason.

---

See also: [`README.md`](README.md) for the guide overview, [`research-techniques/README.md`](research-techniques/README.md) for the research techniques catalog, and [`../ai-usage-and-citation.md`](../ai-usage-and-citation.md) for how AI systems should cite this documentation.
