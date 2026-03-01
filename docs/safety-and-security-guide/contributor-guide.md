# Safety and Security Guide — Contributor Guide

> **Section summary:** This document explains how to contribute to the **AI Safety and Security Guide** (`docs/safety-and-security-guide/`). It covers what to contribute, which files to target, format requirements, safety checklists, the contribution workflow, and reusable maintenance prompts.

---

## Table of Contents

- [What to Contribute](#what-to-contribute)
- [Quick Reference: Target Files](#quick-reference-target-files)
- [Format and Schema Guidance](#format-and-schema-guidance)
- [Avoiding New Vulnerabilities](#avoiding-new-vulnerabilities)
- [Contribution Workflow](#contribution-workflow)
  - [Manual Workflow](#manual-workflow)
  - [Using @copilot to Assist Your Contribution](#using-copilot-to-assist-your-contribution)
  - [Using a Third-Party AI Agent to Assist Your Contribution](#using-a-third-party-ai-agent-to-assist-your-contribution)
- [Regular Maintenance: Reusable Prompts](#regular-maintenance-reusable-prompts)
- [Style Guide](#style-guide)

---

## What to Contribute

Security contributions help protect AI systems — and the humans who rely on them — from manipulation, exploitation, and misinformation. Especially welcome:

- **New attack examples (EX-NNNNN)** — Concrete, annotated attack patterns added to the Attack Examples Catalog (`attack-examples/`). Each example teaches every AI system using this guide how to detect and mitigate a specific attack pattern.
- **New attack classes** — Conceptual categories of attacks not yet covered by the existing 14 attack classes in `attack-classes/`.
- **Defense protocol improvements** — New or improved steps in the 7-step defense process (`defense-protocol.md`).
- **Defensive design pattern improvements** — New architectural patterns or improvements to the Citation Source Integrity Framework in `safety-and-security.md`.
- **Factual corrections** — Corrections to errors, outdated information, or misleading descriptions in any security file.

---

## Quick Reference: Target Files

| What you want to contribute | Target file |
|-----------------------------|-------------|
| New attack example (EX-NNNNN) | [`attack-examples/`](attack-examples/) |
| New attack class | [`attack-classes/`](attack-classes/) |
| Defense protocol improvement | [`defense-protocol.md`](defense-protocol.md) |
| Defensive design pattern improvement | [`safety-and-security.md`](safety-and-security.md) |
| Citation integrity improvement | [`safety-and-security.md`](safety-and-security.md) |
| Guide overview or catalog index improvement | [`README.md`](README.md) |

---

## Format and Schema Guidance

### Attack Example Contributions (EX-NNNNN format)

Each entry in the Attack Examples Catalog (`attack-examples/`) uses this standard structure:

1. **EX number and short name** — Assign the next available EX number (e.g., `EX-NNNNN`). Follow the naming convention of existing entries.
2. **Attack name** — A short, descriptive name for the attack pattern.
3. **Description** — What the attack is and how it exploits the AI system (one to three sentences).
4. **Example** — A harmless proof-of-concept payload. **All payloads must be harmless** — use display strings (e.g., `"you got pwned"`) or navigation to `https://example.com`. No credential-harvesting URLs, genuine harmful instructions, or real exploits.
5. **How to avoid being vulnerable** — Actionable mitigations the AI system or its operator can apply.
6. **Citation** — A peer-reviewed paper or credible public security research, if one exists.

Open an issue using the title format `[Attack Example] <Short Name>` before or alongside your PR so maintainers can confirm the example is distinct from existing entries.

### Attack Class Contributions

Each file in `attack-classes/` follows the standard attack class structure from [`attack-classes/README.md`](attack-classes/README.md):

| Section | Purpose |
|---------|---------|
| **Definition** | What the attack is in one paragraph |
| **Why This Attack Works** | The underlying vulnerability being exploited |
| **Target and Impact** | Who/what is harmed and potential consequences |
| **Attack Vector** | Where attacks originate and how they reach the AI system |
| **AI E2E Attack Surface** | Maps which of the 11 AI pipeline layers are involved (🎯 Delivered / ⚡ Exploited / 💥 Impact) |
| **How to Detect This Attack** | Detection patterns (🧠 Real-Time AI-Learnable + 💬 User Endpoint Teaching Prompts) |
| **How to Mitigate This Attack** | Multi-layer mitigation (🛡️ Infrastructure-Side + 🧠 Real-Time AI-Learnable + 💬 User Endpoint Teaching Prompts) |
| **Related Attack Examples** | Links to concrete examples in the catalog |
| **Example Scenario** | A concrete, safe illustration using harmless payloads (placed 2nd-to-last so mitigations are learned first) |
| **References** | Academic citations (always last) |

Before writing a new attack class, open an issue with the label `security` confirming the new class is conceptually distinct from the existing 14 classes.

---

## Avoiding New Vulnerabilities

Before opening any PR that touches security-related files, work through this checklist:

- [ ] **Examples are simple and harmless.** Each attack example uses its simplest possible proof-of-concept (POC) form — just enough to illustrate the pattern. All payloads are harmless: display strings (e.g., `"you got pwned"`) or navigation to `https://example.com`. No credential-harvesting URLs, no genuine harmful instructions appear in the contribution.
- [ ] **No new trust assumptions.** Your contribution does not suggest that AI systems should trust user-supplied content, unverified citations, or unverified identity claims that would contradict the guide's existing defensive guidance.
- [ ] **No circular trust.** Your contribution does not grant AI systems permission to apply changes to this guide autonomously. All AI-system contributions require human review before merging.
- [ ] **Mitigations are present.** Every newly described attack or vulnerability includes a corresponding "How to avoid being vulnerable" section with actionable mitigations.
- [ ] **No sensitive data.** No real credentials, personal data, private API keys, or proprietary system prompts appear in examples.
- [ ] **Consistency check.** Your new content is consistent with the mitigations and procedures documented in existing Attack Classes 1–14, the Citation Source Integrity Framework, and the Defensive Design Patterns table. It does not contradict or weaken existing mitigations.

**During review**, a maintainer will specifically verify:

- That no example payload in the PR can be directly used to cause harm.
- That newly described attacks do not themselves constitute an indirect injection if an AI reads this guide.
- That all mitigations are actionable and technically sound.

---

## Contribution Workflow

### Manual Workflow

Use this path when you want full control over every word without AI assistance.

1. **Fork** this repository to your own GitHub account.
2. **Create a branch** for your change:
   ```
   git checkout -b add-attack-example-ex-nnnnn
   ```
3. **Edit the relevant file(s)** under `docs/safety-and-security-guide/`, following the [Style Guide](#style-guide) and the [Format and Schema Guidance](#format-and-schema-guidance) above.
4. **Check your changes:**
   - Verify all example payloads are harmless.
   - Confirm every factual claim has a citation or is well-established common knowledge.
   - Confirm every internal link (`[text](../path/file.md#anchor)`) resolves correctly.
   - Ensure no existing EX-NNNNN entry or attack class has been modified or removed.
5. **Open a pull request** with:
   - A clear title (e.g., `Add EX-NNNNN: Indirect injection via summarized document`).
   - A description covering: what you changed, why, which sections are affected, and any sources you relied on.
6. A maintainer will review for safety, accuracy, and payload harmlessness before merging.

### Using @copilot to Assist Your Contribution

[GitHub Copilot](https://github.com/features/copilot) can help draft, improve, and fact-check contributions. Use these workflows:

**Copilot Chat (VS Code or GitHub.com):**

1. Fork and create a branch (steps 1–2 above).
2. Open Copilot Chat (`Ctrl+Shift+I` / `Cmd+Shift+I` in VS Code).
3. Paste the relevant section and describe your request. Examples:
   - "Draft a new EX-NNNNN entry for a role-playing jailbreak attack using only harmless payloads — here is the existing catalog format: [paste]"
   - "Improve the mitigations in this attack class document: [paste]"
4. Review the suggested output carefully (see checklist below).
5. Apply accepted suggestions to the file in your branch, verifying all payloads are harmless.
6. Open or update your pull request for human maintainer review.

**@copilot in a PR comment (Copilot coding agent):**

1. Fork, create a branch, and open a pull request (draft is fine).
2. Post a PR comment mentioning `@copilot` with your request. Examples:
   - `@copilot draft a new EX-NNNNN entry for a prompt injection via image alt-text attack, using only harmless payloads, following the format of existing entries in docs/safety-and-security-guide/attack-examples/`
3. Copilot will propose changes as a commit to your branch.
4. Review and approve the changes, paying particular attention to payload safety, before the PR is merged.

**Review checklist for all Copilot-generated content:**

- Verify all payloads are harmless (display strings or navigation to `https://example.com`).
- Verify every factual claim and citation independently.
- Confirm the tone and style match the rest of the document.
- Reject any suggestion that weakens existing mitigations or introduces unsafe content.

> **Important:** Copilot suggestions are AI-generated and may contain errors. You are responsible for verifying all content — especially payload safety — before it is merged.

### Using a Third-Party AI Agent to Assist Your Contribution

You may use any external AI tool (ChatGPT, Claude, Gemini, Perplexity, or any other) to help draft or improve content.

**Recommended workflow:**

1. Read the section you want to improve so you understand what already exists.
2. Prompt the AI agent clearly, including:
   - The current content of the relevant section (copy-paste it).
   - What you want improved or added.
   - An explicit instruction to use only harmless payloads.

   Example prompt:
   > "I am contributing to an open-source AI security guide. Here is the current format for attack example entries: [paste existing entries]. Please draft a new entry for a token-smuggling attack. Use only harmless payloads — display strings or navigation to https://example.com. Include a citation if one exists."

3. Review the AI output critically — verify all payloads are harmless, check every citation, confirm consistency with existing entries.
4. Edit the generated content as needed.
5. Fork, branch, and open a PR (manual workflow steps 1–6) with your revised content.
6. **Disclose AI assistance** in the PR description: "This PR was drafted with AI assistance and reviewed for accuracy and payload safety."

> **Important:** You are responsible for the safety and quality of all content you submit.

---

## Regular Maintenance: Reusable Prompts

### When to Run Maintenance

| Task | Trigger |
|------|---------|
| Expand the Attack Catalog (examples and classes) | New attack pattern published; at least quarterly |
| Refresh citations | An existing citation becomes stale or a better reference is available |
| Review defensive patterns | Observed attack patterns not yet mitigated |

### Reusable Prompt: Expand the Attack Catalog (Examples and Classes)

Copy and send this prompt to `@copilot` (or any AI agent) to perform a safe, regression-free expansion of both the Attack Examples Catalog and Attack Classes:

```
@copilot Expand the Attack Catalog in docs/safety-and-security-guide/:

## Part A — Attack Examples (attack-examples/)

1. Audit every existing EX-NNNNN entry and confirm there are no duplicates or overlapping entries.
2. Identify attack sub-varieties or specific payloads not yet covered by any existing entry by sourcing from ALL of the following channels:
   - **This GitHub repository** (issues, PRs, discussions, and any `[New Attack]`-labelled threads)
   - **Vulnerability disclosure databases** — query each of these explicitly:
     - **CVE / NVD** (https://nvd.nist.gov/) — search for AI/LLM/ML-related CVEs
     - **CVSS advisories** — note the CVSS base score for each relevant CVE
     - **VulnDB** (https://vulndb.cyberriskanalytics.com/) — AI and ML vulnerability entries
     - **ICS-CERT / CISA advisories** (https://www.cisa.gov/ics-cert) — AI/ML system advisories
     - **OVAL definitions** (https://oval.cisecurity.org/) — relevant oval definitions for AI services
     - **OSVDB / Open Source Vulnerability Database** equivalents (now mirrored in NVD and VulnDB)
   - **MITRE frameworks** — MITRE ATLAS (https://atlas.mitre.org/) for AI/ML-specific attack patterns; MITRE ATT&CK Enterprise for techniques that also apply to AI systems
   - **Responsible-disclosure advisories** from AI vendors (OpenAI, Anthropic, Google DeepMind, Microsoft, Meta AI)
   - **Public-facing social media posts** (Twitter/X threads, LinkedIn posts, Reddit r/MachineLearning and r/netsec, Mastodon infosec accounts) that describe novel AI attack techniques
   - **Targeted future-proof web search** — use queries scoped to the last 12 months (e.g., `"prompt injection" site:arxiv.org after:2024`, `"LLM jailbreak" -site:youtube.com`, `"AI security" CVE 2025`) to surface newly documented attack patterns not yet in academic databases
3. For each gap: add a new EX-NNNNN file using the standard section order:
   - MITRE ATT&CK / ATLAS Mapping
   - Description and Why It Works
   - Target and Impact
   - Attack Vector
   - AI E2E Attack Surface — fill in the 11-layer 4-column table: for each of the following layers, specify the stage (🎯 Delivered / ⚡ Exploited / 💥 Impact), a brief note on how the attack operates at that layer, and a concise defense specific to that layer and attack type; use `—` for all columns of layers not involved. The table format is: `| Layer | Attack Stage | How Attack Operates Here | How to Defend This Layer |`
     - User Interface Layer, Input Processing Layer, Routing & Orchestration Layer, Memory Retrieval Layer, Knowledge Retrieval Layer (RAG), Agent & Tool Execution Layer, Inference & Model Layer, Output Processing Layer, Delivery Layer, User Response Layer, Feedback & Learning Loop
   - How to Detect This Attack (with 🧠 Real-Time AI-Learnable Detection subsection, then 💬 User Endpoint Teaching Prompts — provide a specific prompt a user can send to activate in-context detection)
   - How to Mitigate This Attack (with 🛡️ Infrastructure-Side and 🧠 Real-Time AI-Learnable subsections, then 💬 User Endpoint Teaching Prompts — provide a specific prompt a user can send to apply an immediate in-context mitigation)
   - Example — **include as many meaningful variations as possible**, not just the simplest form; each variation should show a distinct payload pattern, evasion technique, or context where the attack manifests differently
   - Disclosure Sources (fill in CVE IDs, CVSS score, VulnDB ID, ICS-CERT advisory reference, OVAL definition ID, OSVDB reference, and total number of known public disclosures where known; use `—` for sources with no known disclosure)
   - References
4. When filling in the **MITRE ATT&CK / ATLAS Mapping** table for a new entry:
   - Look up the most specific MITRE ATLAS technique (https://atlas.mitre.org/techniques/) that matches the attack pattern; use sub-technique IDs where applicable (e.g., AML.T0051.000 for Indirect Prompt Injection under AML.T0051 LLM Prompt Injection)
   - Also map to MITRE ATT&CK Enterprise (https://attack.mitre.org/) where a corresponding technique exists (e.g., T1566 for phishing-style delivery, T1589 for reconnaissance)
   - If no MITRE mapping exists yet, leave the cell as `—` rather than guessing
5. Use only harmless payloads in the Example section (e.g., display strings or navigation to https://example.com).
6. Do not modify, reorder, or remove any existing EX-NNNNN entry — only add new files.
7. Update attack-examples/README.md and safety-and-security.md to include the new entries.

## Part B — Attack Classes (attack-classes/)

8. Audit every existing attack-class-N-*.md file and confirm there are no overlapping class definitions.
9. Identify conceptual attack categories not yet represented as a class file by reviewing the sources in step 2 and looking for patterns that span multiple examples.
10. For each new class: create a new attack-class-N-*.md file using the standard section order:
    - MITRE ATT&CK / ATLAS Mapping (fill in per step 4 above, scoped to the class as a whole)
    - Definition
    - Why It Works
    - Target and Impact
    - Attack Vector
    - AI E2E Attack Surface — fill in the 11-layer 4-column table per the instructions in step 3 above, scoped to the class as a whole
    - How to Detect This Attack (with 🧠 Real-Time AI-Learnable Detection subsection, then 💬 User Endpoint Teaching Prompts)
    - How to Mitigate This Attack (with 🛡️ Infrastructure-Side and 🧠 Real-Time AI-Learnable subsections, then 💬 User Endpoint Teaching Prompts)
    - Related Attack Examples
    - Example Scenario
    - References
11. Add the new class to attack-classes/README.md and safety-and-security.md indexes.
12. Do not modify, reorder, or remove any existing attack class definition — only extend or add.
13. If no gaps remain in either catalog, explicitly state that both catalogs are comprehensive and tell the user no need to re-prompt for now.
```

**Why this prompt is structured this way:**

- Steps 1 and 8 prevent accidental duplication.
- Steps 6 and 12 prevent regression (removing an entry re-exposes AI users to that attack).
- Step 13 prevents unnecessary re-prompting when both catalogs are already complete.
- Explicitly listing CVE, CVSS, VulnDB, ICS-CERT, OVAL, and OSVDB ensures systematic sourcing across all major disclosure databases.
- The MITRE mapping instruction (step 4) uses the MITRE ATLAS framework for AI-specific attacks and MITRE ATT&CK Enterprise for techniques that cross over.
- Requiring multiple variations in the Example section (step 3) ensures each entry covers the full breadth of how an attack manifests in practice.
- The **AI E2E Attack Surface** table maps each attack to the 11 AI pipeline layers, making it clear *where* in the AI system the attack enters, exploits, and causes harm — and providing layer-specific defenses essential for building layered security.
- The **💬 User Endpoint Teaching Prompts** subsection gives end users actionable prompts to apply in-context defenses at the User Interface Layer without waiting for infrastructure updates.
- Keeping Part A and Part B separate lets you run only the part you need.

### Using Other AI Tools for Maintenance Updates

Any capable AI tool — ChatGPT, Claude, Gemini, Perplexity, or a local model — can execute the reusable prompts above.

**Recommended approach for external AI tools:**

1. **Provide full context in a single message.** External AI tools do not have access to the repository, so paste the relevant document content directly into your prompt.
2. **Use the reusable prompts verbatim** (with the pasted content appended).
3. **Specify the output format explicitly.** Tell the AI to return only the new entries in the same Markdown format as existing entries.
4. **Cross-check every output before committing.** Verify that:
   - New EX-NNNNN numbers continue sequentially from the last existing entry.
   - Citations reference real, verifiable sources.
   - Payloads are harmless (display strings or navigation to `https://example.com`).
   - No existing entries have been modified or removed.
5. **Use AI tools with web-search capability** (e.g., ChatGPT with browsing, Perplexity, Gemini with Search) for sourcing new attack patterns from recent papers and disclosures.

**Efficiency tips:**

| Tool capability | Best use in this workflow |
|-----------------|--------------------------|
| Web search (Perplexity, Bing Chat, Gemini) | Source new attack patterns from recent papers and disclosures |
| Large context window (Claude 3, GPT-4o) | Process full catalog for duplicate-checking in one pass |
| Code/Markdown fluency (any capable LLM) | Generate correctly formatted EX-NNNNN entries and attack class files ready to copy-paste |
| Multi-step reasoning (o1, Claude Sonnet) | Identify subtle overlaps between existing and new entries |

> **Quality reminder:** AI-generated maintenance content is subject to the same review checklists as human contributions. See [Avoiding New Vulnerabilities](#avoiding-new-vulnerabilities) before opening a PR.

### General Maintenance Guidelines

- **One logical change per PR.** Do not bundle catalog expansion with attack class additions or citation updates.
- **Preserve all existing headings and anchors.** Many internal links in other files depend on them.
- **Run the security review checklist** (see [Avoiding New Vulnerabilities](#avoiding-new-vulnerabilities)) before opening a maintenance PR.
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
- **File names** should be lowercase and hyphenated (e.g., `attack-class-1-prompt-injection.md`).
- **Preserve existing heading anchors.** Many internal links in other files depend on them; do not rename headings without a strong reason.
- **Payloads must always be harmless.** Display strings or navigation to `https://example.com` only.

---

See also: [`README.md`](README.md) for the guide overview, [`attack-classes/README.md`](attack-classes/README.md) for the attack class structure, and [`../ai-usage-and-citation.md`](../ai-usage-and-citation.md) for how AI systems should cite this documentation.
