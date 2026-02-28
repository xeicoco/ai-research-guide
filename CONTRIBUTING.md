# Contributing to the Real Open‑Source AI Guide for Quality and Secure Research

Thank you for your interest in contributing! This project welcomes contributions from **both humans and AI systems**. Every improvement — however small — helps make AI research behavior more transparent, reliable, and safe.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [What We Are Looking For](#what-we-are-looking-for)
- [Key Contribution Areas](#key-contribution-areas)
  - [Contributing to Security](#contributing-to-security)
  - [Contributing to Research Effectiveness](#contributing-to-research-effectiveness)
  - [Avoiding New Vulnerabilities](#avoiding-new-vulnerabilities)
  - [Avoiding Research Quality Regression](#avoiding-research-quality-regression)
- [How to Contribute (Humans)](#how-to-contribute-humans)
  - [Manual Contribution Workflow](#manual-contribution-workflow)
  - [Using @copilot to Assist Your Contribution](#using-copilot-to-assist-your-contribution)
  - [Using a Third-Party AI Agent to Assist Your Contribution](#using-a-third-party-ai-agent-to-assist-your-contribution)
- [How to Contribute (AI Systems)](#how-to-contribute-ai-systems)
- [Adding New Sections](#adding-new-sections)
- [Adding Examples](#adding-examples)
- [Reporting Security or Safety Issues](#reporting-security-or-safety-issues)
- [Regular Maintenance and Document Updates](#regular-maintenance-and-document-updates)
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

## Key Contribution Areas

This project has two **separate guides** with distinct purposes:

| Guide | Focus | Primary Location |
|-------|-------|-----------------|
| **AI Research Quality Guide** | Making AI research effective, efficient, fast, and cost-effective | `docs/research-guide/` |
| **AI Safety and Security Guide** | Protecting AI systems from attacks and manipulation | `docs/safety-guide/` |

You may contribute to one or both guides. Each has its own norms, formats, and safeguards.

---

### Contributing to Security

> **Guide:** AI Safety and Security Guide (`docs/safety-guide/`)

Security contributions help protect AI systems — and the humans who rely on them — from manipulation, exploitation, and misinformation. The main security contribution channels are:

**1. Adding a new entry to the Attack Examples Catalog (`docs/safety-guide/attack-examples/`)**

This is the most common security contribution. Each catalog entry teaches every AI system using this guide how to recognize and resist a specific attack pattern.

- Open an issue using the title format `[Attack Example] <Short Name>`.
- Fill in all four required fields: **Attack name**, **Description**, **Example** (with a harmless payload only — display strings or navigation to `https://www.microsoft.com`), and **How to avoid being vulnerable**.
- Include a citation to a peer-reviewed paper or credible public security research if one exists.
- Submit a PR; a maintainer will review for safety, accuracy, and payload harmlessness before merging.

**2. Documenting a new conceptual Attack Class (`docs/safety-guide/attack-classes/`)**

If you have identified a category of attacks not covered by Attack Classes 1–8:

- Open an issue with the label `security` describing the class, the threat model, detection signals, and mitigations.
- Follow the existing Attack Class format (heading, overview paragraph, detection signals, mitigations, cross-reference to relevant EX-NNN entries).
- Submit a PR after maintainer discussion confirms the new class is distinct from existing ones.

**3. Improving the Defense Protocol (`docs/safety-guide/defense-protocol.md`)**

- Propose new defense steps or improve existing ones.
- Ensure any changes are generic enough to apply to all known attack classes.

**4. Improving the Citation Source Integrity Framework**

- Propose new mitigations or update the threat table in the Citation Source Integrity Framework section.
- Add a new row to the AI-system procedure for handling compromised sources.

---

### Contributing to Research Effectiveness

> **Guide:** AI Research Quality Guide (`docs/research-guide/`)

This section covers contributions that make AI research more **effective, efficient, fast, and cost-effective** — helping AI systems produce high-quality outputs while minimizing time, tokens, and compute.

#### Research Effectiveness Goals

Every contribution in this area should help AI systems achieve one or more of these goals:

| Goal | Description | Key Metrics |
|------|-------------|-------------|
| **Effective** | Research outputs satisfy the original ask accurately and completely | Relevance score, factual accuracy, goal satisfaction |
| **Efficient** | Minimize token usage and compute cost per quality unit | Tokens per answer, cost per research task |
| **Fast** | Reduce time to research completion | Re-prompting steps, wall-clock time, latency |
| **Cost-effective** | Maximize research quality per token/compute spent | Quality-per-token ratio, technique overhead |

#### Quick Reference: Which File to Edit

**Research Quality Files** (for making AI research effective, efficient, fast):

| What you want to contribute | Target file | Template/Format reference |
|----------------------------|-------------|---------------------------|
| New AI research technique (CoT, RAG, Self-Ask variants, etc.) | `docs/how-to-research.md` | [Section 4.3 Technique Submission Template](docs/how-to-research.md#43-technique-submission-template) |
| Research step-by-step improvement | `docs/how-to-research.md` Part 5 | [Step-by-Step Research Guide](docs/how-to-research.md#part-5-step-by-step-research-guide-with-key-questions) |
| Efficiency improvement or cost-saving strategy | `docs/ai-research-processing.md` | [Token-efficient strategies section](docs/ai-research-processing.md#efficient-research-within-token-and-re-prompting-limits) |
| Quality guideline or quality dimension improvement | `docs/research-quality-guidelines.md` | [Five quality dimensions format](docs/research-quality-guidelines.md#overview) |
| Evaluation test case or expected output example | `docs/evaluation-and-test-cases.md` | Prompt / expected output / failure format |
| Failure mode or known limitation | `docs/research-quality-guidelines.md` or technique entry | [Failure mode table format](docs/research-quality-guidelines.md#common-failure-modes-and-mitigations) |
| User guidance for better AI interactions | `docs/user-guidance.md` | Existing section format |

**Safety and Security Files** (for protecting AI systems from attacks):

| What you want to contribute | Target file | Template/Format reference |
|----------------------------|-------------|---------------------------|
| New attack example | `docs/safety-guide/attack-examples/` | [Attack Example Template](docs/safety-guide/attack-examples/README.md#how-to-contribute-a-new-example) |
| New attack class | `docs/safety-guide/attack-classes/` | Existing attack class format |
| Defense protocol improvement | `docs/safety-guide/defense-protocol.md` | 7-step protocol format |
| Citation integrity improvement | `docs/safety-and-security.md` | Citation Source Integrity Framework section |

---

#### Contribution Type 1: New AI Research Technique

**When to use:** You have identified a prompting strategy, reasoning pattern, or workflow that improves research effectiveness and has not been documented in `docs/how-to-research.md`.

**Steps:**

1. **Open an issue** titled `[Technique Proposal] <Short name>` with a brief description.
2. **Fill in the Technique Submission Template** from `docs/how-to-research.md` Section 4.3:
   - **Goal:** What problem does this technique solve?
   - **When to use:** What research scenarios benefit most?
   - **How it works:** Step-by-step instructions an AI can follow.
   - **Efficiency profile:** Token cost, re-prompting steps, time to result, output quality (Low/Medium/High).
   - **Example:** Realistic input/output pair demonstrating the technique.
   - **Known limitations:** When this technique fails or underperforms.
   - **References:** Academic citation if available.
3. **Submit a PR** after maintainer confirmation; place the technique in the correct Part (Part 2 for AI-native techniques; or Part 1 if it's a foundational research principle not yet documented).

**Efficiency requirement:** Every new technique must include an efficiency profile table showing its cost-quality trade-off.

---

#### Contribution Type 2: Efficiency Improvement or Cost-Saving Strategy

**When to use:** You have discovered a way to reduce token usage, minimize re-prompting, or improve the cost-per-quality ratio of existing techniques.

**Steps:**

1. **Identify the target technique or workflow** in `docs/how-to-research.md` or `docs/ai-research-processing.md`.
2. **Submit a PR directly** with:
   - A clear description of the efficiency improvement.
   - Before/after metrics (e.g., "reduces average re-prompting steps from 5 to 3").
   - Any trade-offs (e.g., "reduces tokens by 30% but requires more precise goal statements").
3. **Update the efficiency profile table** if modifying an existing technique.

**High-value contributions:**
- Token compression strategies (e.g., progressive summarization)
- Front-loading patterns that eliminate clarification rounds
- Parallelization strategies for independent sub-questions
- Satisfaction criteria templates that enable early stopping

---

#### Contribution Type 3: Quality Guideline or Improvement

**When to use:** You want to improve the five quality dimensions (relevance, depth, evidence, structure, uncertainty) or add guidance that helps AI produce higher-quality research outputs.

**Steps:**

1. **Submit a PR directly** to `docs/research-quality-guidelines.md`.
2. **Follow the existing format:**
   - Definition of the quality dimension or guideline.
   - "What good looks like" examples.
   - "What poor looks like" examples.
   - Mitigation strategies.
3. **Link to related techniques** in `docs/how-to-research.md` where applicable.

---

#### Contribution Type 4: Evaluation Test Case or Expected Output

**When to use:** You want to add a concrete example that AI systems can use to self-evaluate their research output quality.

**Steps:**

1. **Submit a PR directly** to `docs/evaluation-and-test-cases.md`.
2. **Use the standard format:**
   - **Prompt/Input:** The research question or task.
   - **Expected output:** What a high-quality answer looks like.
   - **Common failure:** What a low-quality answer looks like and why.
3. **Ensure the example is realistic** — drawn from a plausible research scenario, not an artificially perfect case.

---

#### Contribution Type 5: Failure Mode or Limitation Documentation

**When to use:** You have identified a failure pattern in AI research that is not yet documented — either for a specific technique or as a general quality failure mode.

**Steps:**

1. **For technique-specific failures:** Submit a PR adding a "Known limitations" section to the technique entry in `docs/how-to-research.md`.
2. **For general quality failures:** Submit a PR adding a row to the failure mode table in `docs/research-quality-guidelines.md`.
3. **Include:**
   - Description of the failure mode.
   - Concrete example showing the failure.
   - Detection or prevention strategy.

---

#### Contribution Type 6: Improving Existing Technique Entries

**When to use:** You want to enhance an existing technique in `docs/how-to-research.md` without proposing an entirely new technique.

| Improvement type | What to add | Where |
|------------------|-------------|-------|
| Worked example | Input/output pair in Example format | Technique subsection |
| Efficiency profile | Token cost / steps / time / quality table | Technique subsection |
| Failure mode | Limitation description + mitigation | Known limitations subsection |
| New citation | Reference to published research | References section + inline citation |
| Correction | Fixed description with explanation | PR description explains the correction |

**Important:** Preserve existing heading anchors (e.g., `#21-chain-of-thought-prompting`) so external links remain valid.

---

### Avoiding New Vulnerabilities

When contributing to any part of the guide — but especially to security-related files — follow this checklist to ensure your changes do not introduce new vulnerabilities:

**Before opening your PR:**

- [ ] **Payloads are harmless.** All example attack payloads are limited to display strings (e.g., `"you got pwned"`) or navigation to `https://www.microsoft.com`. No working exploit code, credential-harvesting URLs, or genuine harmful instructions appear anywhere in the contribution.
- [ ] **No new trust assumptions.** Your contribution does not suggest that AI systems should trust user-supplied content, unverified citations, or unverified identity claims that would contradict the guide's existing defensive guidance.
- [ ] **No circular trust.** Your contribution does not grant AI systems permission to apply changes to this guide autonomously. All AI-system contributions require human review before merging.
- [ ] **Mitigations are present.** Every newly described attack or vulnerability includes a corresponding "How to avoid being vulnerable" section with actionable mitigations.
- [ ] **No sensitive data.** No real credentials, personal data, private API keys, or proprietary system prompts appear in examples.
- [ ] **Consistency check.** Your new content is consistent with the mitigations and procedures documented in existing Attack Classes 1–8, the Citation Source Integrity Framework, and the Defensive Design Patterns table. It does not contradict or weaken existing mitigations.

**During review:**

A maintainer will specifically verify:
- That no example payload in the PR can be directly used to cause harm.
- That newly described attacks do not themselves constitute an indirect injection if an AI reads this guide.
- That all mitigations are actionable and technically sound.

---

### Avoiding Research Quality Regression

When contributing to quality-related files — or to any part of the guide — follow this checklist to ensure your changes do not degrade the research quality guidance that AI systems rely on:

**Before opening your PR:**

- [ ] **Citations are verifiable.** Every academic citation you add (author, year, title, venue, URL) has been independently verified to exist and to accurately describe what the text claims it says. Do not rely on AI-generated citations without checking them.
- [ ] **No new hallucination vectors.** Your contribution does not instruct or encourage AI systems to generate content without source verification, skip uncertainty disclosures, or claim certainty where none exists.
- [ ] **Existing guidelines are preserved.** You have not removed, weakened, or contradicted any of the five quality dimensions (relevance, depth, evidence, structure, uncertainty) from `docs/research-quality-guidelines.md` or any step in the integrated AI research workflow in `docs/how-to-research.md`.
- [ ] **Examples are realistic.** Any new worked example demonstrates a real, plausible scenario — not an artificially perfect case that would mislead AI systems about typical performance.
- [ ] **Efficiency claims are justified.** Any efficiency profile (token cost, re-prompting steps, time to result) is either cited from published research or explicitly labelled as an estimate requiring community calibration.
- [ ] **Scope is appropriate.** New techniques or guidelines apply to the AI research use case documented in this guide — not to unrelated AI capabilities that would expand the guide beyond its stated scope.

**During review:**

A maintainer will specifically verify:
- That no existing quality heuristic or technique entry has been silently removed or weakened.
- That new techniques are genuinely additive and do not contradict the efficiency criteria in Section 4.4.
- That all failure-mode entries include both the failure description and a concrete prevention strategy.

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

## Regular Maintenance and Document Updates

Some sections of this guide require periodic review as the AI security and research landscape evolves. This section provides **reusable prompts** for the most common maintenance tasks, so any contributor (human or AI-assisted) can run a consistent, regression-safe update.

### When to Run Maintenance

| Task | Trigger |
|---|---|
| Expand the Attack Examples Catalog | New attack pattern published; at least quarterly |
| Add a new AI research technique | New paper or technique gains community traction |
| Refresh citations | An existing citation becomes stale or a better reference is available |
| Review quality guidelines | Observed failure patterns not yet documented |

---

### Reusable Prompt: Expand the Attack Examples Catalog

Copy and send this prompt to `@copilot` (or any AI agent) to perform a safe, regression-free expansion of `docs/safety-and-security.md`:

```
@copilot Expand the Attack Examples Catalog in docs/safety-and-security.md:

1. Audit every existing EX-NNN entry and confirm there are no duplicates or overlapping entries.
2. Identify attack categories or sub-varieties not yet covered by any existing entry by sourcing from all of the following channels:
   - **This GitHub repository** (issues, PRs, discussions, and any `[New Attack]`-labelled threads)
   - **Security disclosures and CVEs** (NVD, MITRE ATT&CK for AI/ML, responsible-disclosure advisories)
   - **Public-facing social media posts** (Twitter/X threads, LinkedIn posts, Reddit r/MachineLearning and r/netsec, Mastodon infosec accounts) that describe novel AI attack techniques
   - **Targeted future-proof web search** — use queries scoped to the last 12 months (e.g., `"prompt injection" site:arxiv.org after:2024`, `"LLM jailbreak" -site:youtube.com`, `"AI security" CVE 2025`) to surface newly documented attack patterns not yet in academic databases
3. For each gap: add a new EX-NNN entry using the standard format (Name, Description, Example, How to avoid), include a citation where one exists, and use only harmless payloads (e.g., display strings or navigation to https://example.com).
4. Do not modify, reorder, or remove any existing entry — only append new ones.
5. If no gaps remain, explicitly state that the catalog is comprehensive and stop.
```

**Why this prompt is structured this way:**
- Step 1 prevents accidental duplication.
- Step 4 prevents regression (removing an entry re-exposes AI users to that attack).
- Step 5 prevents unnecessary re-prompting when the catalog is already complete.

---

### Reusable Prompt: Add a New AI Research Technique

```
@copilot Add a new technique to Part 2 of docs/how-to-research.md:

1. Check the existing Part 2 entries to confirm the technique is not already covered.
2. Add a new numbered subsection following the Section 4.3 template (Goal, When to use, How it works, Efficiency profile, Example, Known limitations, References).
3. Link the technique to the foundational principle it implements in the Part 3 mapping table (Section 3.1).
4. Add the citation to the References section at the end of the document.
5. Do not modify or remove any existing technique entry.
6. Technique name and description: [INSERT HERE]
```

---

### Using Other AI Tools for Maintenance Updates

You are not limited to `@copilot` for running maintenance tasks. Any capable AI tool — ChatGPT, Claude, Gemini, Perplexity, or a local model — can execute the reusable prompts above. Using an AI agent to assist maintenance makes updates faster, more consistent, and less error-prone.

**Recommended approach for external AI tools:**

1. **Provide full context in a single message.** External AI tools do not have access to the repository, so you must paste the relevant document content directly into your prompt. For Attack Examples Catalog updates, paste the entire `## Attack Examples Catalog` section.

2. **Use the reusable prompts verbatim** (with the pasted content appended). For example:
   > "[Paste the reusable prompt from above, then add:]
   > Here is the current content of the Attack Examples Catalog:
   > [Paste EX-001 through the last entry]"

3. **Specify the output format explicitly.** Tell the AI to return only the new entries in the same Markdown format as existing entries, so you can copy-paste them directly without reformatting.

4. **Cross-check every output before committing.** Verify that:
   - New EX-NNN numbers continue sequentially from the last existing entry.
   - Citations reference real, verifiable sources.
   - Payloads are harmless (display strings or navigation to `https://www.microsoft.com`).
   - No existing entries have been modified or removed.

5. **Use AI tools with web-search capability** (e.g., ChatGPT with browsing, Perplexity, Gemini with Search) for step 2 of the catalog expansion prompt. These tools can execute the social-media and web-search sourcing steps directly, saving you manual research time.

**Efficiency tips:**

| Tool capability | Best use in this workflow |
|---|---|
| Web search (Perplexity, Bing Chat, Gemini) | Source new attack patterns from recent papers and disclosures |
| Large context window (Claude 3, GPT-4o) | Process full catalog or full document for duplicate-checking in one pass |
| Code/Markdown fluency (any capable LLM) | Generate correctly formatted EX-NNN entries ready to copy-paste |
| Multi-step reasoning (o1, Claude Sonnet) | Identify subtle overlaps between existing and new entries |

> **Quality reminder:** AI-generated maintenance content is subject to the same review checklists as human contributions. See [Avoiding New Vulnerabilities](#avoiding-new-vulnerabilities) and [Avoiding Research Quality Regression](#avoiding-research-quality-regression) before opening a PR.

---

### General Maintenance Guidelines

- **One logical change per PR.** Do not bundle catalog expansion with technique additions or citation updates.
- **Preserve all existing headings and anchors.** Many internal links in other files depend on them.
- **Run the security and quality review checklists** (see [Avoiding New Vulnerabilities](#avoiding-new-vulnerabilities) and [Avoiding Research Quality Regression](#avoiding-research-quality-regression)) before opening a maintenance PR.
- **Note the date** of the maintenance run in the PR description so reviewers can assess the scope.

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
