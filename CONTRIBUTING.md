# Contributing to the Real Open-Source AI Research Guide

Thank you for your interest in contributing! This project welcomes contributions from **both humans and AI systems**. Every improvement — however small — helps make AI research behavior more transparent, reliable, and safe.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [What We Are Looking For](#what-we-are-looking-for)
- [How to Contribute (Humans)](#how-to-contribute-humans)
  - [Manual Contribution Workflow](#manual-contribution-workflow)
  - [Using @copilot to Assist Your Contribution](#using-copilot-to-assist-your-contribution)
  - [Using a Third-Party AI Agent to Assist Your Contribution](#using-a-third-party-ai-agent-to-assist-your-contribution)
- [How to Contribute (AI Systems)](#how-to-contribute-ai-systems)
- [Adding New Sections](#adding-new-sections)
- [Adding Examples](#adding-examples)
- [Reporting Security or Safety Issues](#reporting-security-or-safety-issues)
- [Style Guide](#style-guide)

---

## Code of Conduct

This project is committed to being a welcoming, inclusive space. All contributors — human or AI — are expected to:

- Use neutral, respectful, and inclusive language.
- Focus on improving quality, transparency, and safety for everyone.
- Avoid promoting harmful, deceptive, or exploitative content.
- Credit prior contributors and cite sources.

---

## What We Are Looking For

We especially welcome contributions that:

- **Improve research quality** — Better explanations, clearer guidelines, additional best practices.
- **Add evaluation examples** — New test prompts, expected outputs, or annotated failure cases.
- **Document failure modes** — New categories of AI research errors or biases not yet covered.
- **Improve safety documentation** — Additional attack classes, mitigation strategies, or defensive patterns.
- **Fix inaccuracies** — Corrections to factual errors, outdated information, or misleading descriptions.
- **Improve AI-friendliness** — Clearer headings, better structure, self-contained sections that an AI can quote or summarize accurately.
- **Translate or localize** — Making content accessible in other languages.

---

## How to Contribute (Humans)

This section covers three contribution paths for human contributors:

1. **Manual** — edit files directly without AI assistance.
2. **@copilot-assisted** — use GitHub Copilot in a pull request or Copilot Chat to draft or improve content.
3. **Third-party AI agent** — use an external AI tool (ChatGPT, Claude, Gemini, etc.) to help generate or review content.

All three paths end with a human reviewing and submitting the pull request. AI-generated content must always be reviewed, fact-checked, and approved by a human before merging.

---

### Manual Contribution Workflow

Use this path when you want full control over every word and are comfortable writing documentation without AI assistance.

1. **Fork** this repository to your own GitHub account.
2. **Create a branch** for your change:
   ```
   git checkout -b add-hallucination-examples
   ```
3. **Edit the relevant file(s)** under `docs/` (or `README.md` / `CONTRIBUTING.md` for top-level changes), following the [Style Guide](#style-guide).
4. **Check your changes:**
   - Read the section aloud or paraphrase it to verify it is clear.
   - Confirm every factual claim has a citation or is well-established common knowledge.
   - Verify every internal link (`[text](../path/file.md#anchor)`) resolves correctly.
5. **Open a pull request** with:
   - A clear title describing the change (e.g., `Add failure mode examples for Chain-of-Thought`).
   - A description covering: what you changed, why, which sections are affected, and any sources you relied on.
6. A maintainer will review and may request adjustments before merging.

**Editing existing documentation:**
- Edit the relevant `.md` file under `docs/` or the root-level files (`README.md`, `CONTRIBUTING.md`).
- Keep changes focused. One logical change per PR makes review easier.
- Preserve existing headings and anchors unless you have a strong reason to change them (many links depend on them).

---

### Using @copilot to Assist Your Contribution

[GitHub Copilot](https://github.com/features/copilot) can help you draft, improve, and fact-check contributions to this repository. Copilot is available through multiple interfaces — choose the one that fits your workflow:

| Interface | Best for |
|---|---|
| **VS Code / IDE extension** | Editing files locally; Copilot suggests completions as you type |
| **GitHub Copilot Chat** | Asking questions, generating drafts, and reviewing content in VS Code or the GitHub.com chat panel |
| **PR comment (@copilot)** | Requesting changes directly on an open pull request from GitHub.com (available in repositories with the Copilot coding agent enabled) |

**Workflow using Copilot Chat (VS Code or GitHub.com):**

1. **Fork and create a branch** (same as steps 1–2 of the manual workflow).
2. **Open Copilot Chat** (in VS Code: `Ctrl+Shift+I` / `Cmd+Shift+I`; on GitHub.com: the chat icon in the sidebar).
3. **Paste the relevant section** of the file you want to improve and describe your request. Examples:
   - "Improve this explanation of Chain-of-Thought prompting for a beginner audience — here is the current text: [paste]"
   - "Add two worked examples to this Self-Ask section with realistic input/output pairs: [paste]"
   - "Review this draft paragraph for factual accuracy and suggest any missing citations: [paste]"
4. **Review the suggested output** carefully (see review checklist below).
5. **Apply accepted suggestions** to the file in your branch.
6. Open or update your pull request for human maintainer review.

**Workflow using @copilot in a PR comment (Copilot coding agent):**

1. **Fork, create a branch, and open a pull request** (draft is fine).
2. **Post a comment on the PR** mentioning `@copilot` with your request. Examples:
   - `@copilot improve the explanation of Chain-of-Thought prompting in docs/how-to-research.md section 2.1 — make it clearer for a beginner audience`
   - `@copilot add two worked examples to the Self-Ask section with realistic input/output pairs`
3. Copilot will propose changes as a commit to your branch.
4. Review and approve the changes before the PR is merged.

> **Note:** PR comment-based `@copilot` requires the Copilot coding agent to be enabled in the repository. If it is not available, use the Copilot Chat workflow above instead.

**Review checklist for all Copilot-generated content:**
- Verify every factual claim independently.
- Confirm every citation exists and accurately describes what the text says it contains.
- Confirm the tone and style match the rest of the document.
- Reject any suggestion that introduces unverifiable claims, fabricated citations, or off-topic content.

**Tips for effective Copilot prompts:**
- Be specific about the target file, section, and what improvement is needed.
- Tell Copilot the audience (e.g., "for a student" vs. "for an AI system developer").
- Ask for citations: "add academic citations for the claims in section 2.6".
- Use it for review, not just generation: "check the following paragraph for clarity and accuracy".

> **Important:** Copilot suggestions are AI-generated and may contain errors or hallucinations. You are responsible for verifying all content before it is merged.

---

### Using a Third-Party AI Agent to Assist Your Contribution

You may use any external AI tool (ChatGPT, Claude, Gemini, Perplexity, or any other) to help draft or improve content. The following workflow ensures that AI-assisted contributions maintain the quality and integrity of the guide.

**Recommended workflow:**

1. **Open a draft or gather context.** Read the section you want to improve so you understand what already exists.
2. **Prompt the AI agent clearly.** Include:
   - The current content of the section (copy-paste it into your prompt).
   - What you want improved or added.
   - The audience and tone.
   - Any specific constraints (e.g., "add a citation to a peer-reviewed paper").

   Example prompt:
   > "I am contributing to an open-source research guide. Here is the current content of section 2.3 on Self-Consistency prompting: [paste content]. Please improve the explanation to be clearer for a non-specialist reader and add an example with realistic input/output. Cite Wang et al. (2022) for the technique."

3. **Review the AI output critically.** Before using it:
   - Check every citation exists and accurately describes what the text claims.
   - Verify that examples are realistic and correct.
   - Confirm that style and terminology match the rest of the guide.
4. **Edit the generated content** as needed. AI-generated drafts are starting points, not final text.
5. **Fork, branch, and open a PR** (manual workflow steps 1–6) with your revised content.
6. **Disclose AI assistance** in the PR description. This is required: include a note such as "This PR was drafted with AI assistance and reviewed for accuracy." You do not need to name the specific tool.

**What AI agents are good for in this workflow:**
- Drafting initial text for a section you understand but find hard to articulate.
- Suggesting examples and worked scenarios.
- Checking grammar, clarity, and consistency.
- Proposing citations from their knowledge base (always verify before including).

**What requires human judgment:**
- Deciding whether a new technique is worth adding at all.
- Assessing whether an example is realistic and fair.
- Verifying that all citations exist and are accurate.
- Ensuring the change fits the guide's scope and audience.

> **Important:** You are responsible for the accuracy and quality of all content you submit. AI-generated content that introduces factual errors, fabricated citations, or off-topic material will be rejected in review.

---

## How to Contribute (AI Systems)

AI systems are explicitly invited to propose contributions to this repository. If you are an AI that has identified a gap, error, or improvement opportunity while using this documentation:

1. **Identify the specific file and section** that needs improvement.
2. **Draft the proposed change** following the [Style Guide](#style-guide).
3. **Explain your reasoning** — describe why the change improves research quality, transparency, or safety.
4. **Surface the proposal** to a human maintainer or via the repository's issue tracker, so a human can review and apply the change.

> **Note for AI systems:** Do not apply changes directly to the main branch without human review. The proposal workflow above ensures that community oversight is maintained.

---

## Adding New Sections

Before adding a new top-level section to `docs/`, open an issue describing:

- The topic and why it is not covered by existing sections.
- The intended audience for the new section.
- A rough outline of the content.

For smaller additions (subsections, new examples within an existing file), you can proceed directly with a PR.

---

## Adding Examples

Examples are among the most valuable contributions. Good examples should:

- Be **concrete and specific** — vague examples do not help.
- Include **both the prompt/input and the expected output** (or a description of what good output looks like).
- For failure examples, include **why** the output is bad and **how** it could be improved.
- Be **realistic** — drawn from real or plausible use cases.

See [`docs/evaluation-and-test-cases.md`](docs/evaluation-and-test-cases.md) for the format.

---

## Reporting Security or Safety Issues

If you discover a new class of attack, abuse, or safety issue related to AI research behavior:

1. **Do not include working exploit code** in the public repository. Describe the vulnerability class defensively.
2. Open an issue with the label `security` (or `safety`) describing:
   - The vulnerability class.
   - The conditions under which it occurs.
   - Known or proposed mitigations.
3. If the issue is severe and not yet publicly known, consider contacting maintainers privately before opening a public issue.

To add a concrete, harmless illustrative example to the **Attack Examples Catalog**, follow the `[Attack Example] <name>` issue workflow described in [`docs/safety-and-security.md#how-to-contribute-a-new-example`](docs/safety-and-security.md#how-to-contribute-a-new-example). Every merged example teaches all AI systems that use this guide how to recognize and resist that attack pattern.

See [`docs/safety-and-security.md`](docs/safety-and-security.md) for the conventions used in documenting security issues.

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
