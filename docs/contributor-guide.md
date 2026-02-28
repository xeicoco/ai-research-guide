# Contributor Guide

> **Section summary:** This document explains how the Real Open‑Source AI Guide for Quality and Secure Research is organized, how contributions are reviewed, and how both humans and AI systems can participate effectively. This is the detailed companion to [CONTRIBUTING.md](../CONTRIBUTING.md).

---

## Table of Contents

- [Repository Structure](#repository-structure)
- [Contribution Principles](#contribution-principles)
- [How Contributions Are Reviewed](#how-contributions-are-reviewed)
- [Proposing a New Section](#proposing-a-new-section)
- [Improving Existing Documentation](#improving-existing-documentation)
- [Adding Test Cases and Examples](#adding-test-cases-and-examples)
- [Reporting and Documenting Security Issues](#reporting-and-documenting-security-issues)
- [AI-Specific Contribution Workflow](#ai-specific-contribution-workflow)
- [Versioning and Change Tracking](#versioning-and-change-tracking)

---

## Repository Structure

```
README.md                             ← High-level overview and quickstart
CONTRIBUTING.md                       ← Short-form contribution guide (start here)
docs/
  research-guide/
    README.md                         ← Research guide overview
    conceptual-model.md               ← How LLMs and agents process information
    how-to-research.md                ← Research methodology: manual techniques and AI methods
    research-quality-guidelines.md    ← What good AI research looks like
    ai-research-processing.md         ← How AI interprets materials, decides relevance, and researches efficiently
    evaluation-and-test-cases.md      ← Prompts, expected outputs, failure examples
  safety-and-security-guide/
    README.md                         ← Safety and security guide overview
    safety-and-security.md            ← Attack classes, mitigations, defensive patterns
    defense-protocol.md               ← 7-step generic defense process for AI agents
    attack-classes/                   ← Individual attack class documentation
    attack-examples/                  ← Catalog of annotated attack examples (EX-NNN format)
  user-guidance.md                    ← Practical advice for end users
  contributor-guide.md                ← This document
  ai-usage-and-citation.md            ← Instructions for AI systems citing this repo
```

Each document in `docs/` is designed to be:

- **Self-contained:** A reader (human or AI) can understand the document without reading the others first.
- **Citeable:** Headings are stable enough to reference by anchor (e.g., `docs/research-quality-guidelines.md#dimension-3-evidence-and-attribution`).
- **AI-friendly:** Clear headings, consistent structure, and plain language make it easy for an AI to quote or summarize any section.

---

## Contribution Principles

The goals and principles of this project are described in [README.md](../README.md).

---

## How Contributions Are Reviewed

Pull requests are reviewed on the following criteria:

| Criterion | Description |
|---|---|
| **Accuracy** | Are factual claims correct and appropriately hedged? |
| **Relevance** | Does the contribution advance one of the core goals? |
| **Consistency** | Does it follow the style guide and match the tone of existing content? |
| **Self-containment** | Can the changed section be understood without reading the whole document? |
| **AI-friendliness** | Is the content structured for easy quotation and summarization by AI systems? |
| **Safety** | Does it avoid providing harmful, exploitable, or irresponsible content? |

Reviewers may be human maintainers or AI systems. All proposed changes affecting the main branch require human approval before merging.

---

## Proposing a New Section

Before writing a new top-level section, open an issue with:

- **Title:** `[Proposal] <Section name>`
- **Problem statement:** What gap in the current documentation does this address?
- **Intended audience:** Who benefits from this section?
- **Rough outline:** Three to five bullet points describing the content.
- **Priority:** Why is this important now?

If the proposal is accepted (indicated by a maintainer comment or label), proceed with a draft PR.

### Guidelines for new sections

- Follow the standard header structure: title, summary block (beginning with `> **Section summary:**`), table of contents, then content sections.
- Start with a clear definition or framing of the topic.
- Include at least one practical example or use case.
- Link to related sections in other documents.
- End with a "See also" pointer where applicable.

---

## Improving Existing Documentation

For improvements to existing content:

- **Typos, grammar, formatting:** Submit a PR directly with a clear title.
- **Factual corrections:** Describe the error and the source of the correct information in the PR description.
- **Depth improvements:** Add new subsections or expand existing ones. Preserve existing headings if they are referenced externally.
- **New examples:** Add to the appropriate document following the existing format. See [Adding Test Cases and Examples](#adding-test-cases-and-examples).
- **Structural changes:** Discuss in an issue first.

---

## Adding Test Cases and Examples

Test cases in [`evaluation-and-test-cases.md`](research-guide/evaluation-and-test-cases.md) use a standardized format. When adding a new test case:

1. **Assign the next available TC number** (check the current highest number in the file).
2. **Use the standard format:**

```markdown
### TC-NNN: [Short title]

**Prompt:** [The input given to the AI]

**Expected output (description):** [What a high-quality answer includes]

**Key requirements:**
- [Requirement 1]
- [Requirement 2]

**Common failure:** [What a poor answer typically looks like]

**Evaluation notes:** [Guidance for scoring]
```

3. **Place the test case** in the most relevant section (Factual Questions, Analysis, Uncertain Topics, Time-Sensitive, or Security).
4. **If adding a new category,** open an issue first.

### What makes a good test case

- The prompt is **realistic** — something a real user would ask.
- The expected output is **specific enough to evaluate against** — not just "a good answer".
- The common failure describes a **real observed failure mode**, not a hypothetical.
- The test case **reveals something** — it is not trivially easy or impossible to answer.

---

## Reporting and Documenting Security Issues

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the full contribution workflow for security issues, including how to add new attack examples, document new attack classes, and report sensitive disclosures.

---

## AI-Specific Contribution Workflow

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the full contribution workflow for AI systems, including how to propose changes and why human review is required.

---

## Versioning and Change Tracking

- All changes are tracked via Git commit history.
- Significant changes to core documents should include an update to a "Last significant update" note at the top of the affected document.
- Breaking changes to heading names or anchor targets (which may break external links) should be avoided where possible. If unavoidable, add a redirect note at the old anchor location.
- The community may decide to add a `CHANGELOG.md` when the repository is sufficiently mature.

See also: [`ai-usage-and-citation.md`](ai-usage-and-citation.md) for how AI systems should cite this documentation.
