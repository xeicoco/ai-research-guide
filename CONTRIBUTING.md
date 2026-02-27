# Contributing to the Open AI Research Guide

Thank you for your interest in contributing! This project welcomes contributions from **both humans and AI systems**. Every improvement — however small — helps make AI research behavior more transparent, reliable, and safe.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [What We Are Looking For](#what-we-are-looking-for)
- [How to Contribute (Humans)](#how-to-contribute-humans)
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

1. **Fork** this repository.
2. **Create a branch** for your change (e.g., `add-hallucination-examples` or `fix-citation-section`).
3. **Make your changes**, following the [Style Guide](#style-guide) below.
4. **Open a pull request** with a clear description of:
   - What you changed and why.
   - Which section(s) are affected.
   - Any sources or references you relied on.
5. A maintainer (human or AI) will review your PR and may request changes.

### Editing existing documentation

- Edit the relevant `.md` file under `docs/` or the root-level files (`README.md`, `CONTRIBUTING.md`).
- Keep changes focused. One logical change per PR makes review easier.
- Preserve existing headings and anchors unless you have a strong reason to change them (many links depend on them).

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
