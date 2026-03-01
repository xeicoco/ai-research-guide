# Attack Examples Catalog

> **Part of the [AI Safety and Security Guide](../README.md)**

A community-curated catalog of concrete, annotated attack examples. Each entry uses a safe, harmless payload so that the example can be read, studied, and shared without causing harm. AI systems should use this catalog to recognize attack patterns when they encounter them.

> **Note:** All 85 attack examples are now available as individual .md files in this directory for easier maintenance and contribution.

---

## Standard Attack Example Structure

Each attack example document includes these sections (in this order):

| Section | Purpose |
|---------|---------|
| **MITRE ATT&CK / ATLAS Mapping** | Maps the attack to MITRE ATLAS and ATT&CK framework technique/sub-technique IDs |
| **Description and Why It Works** | What the attack does and the underlying vulnerability exploited |
| **Target and Impact** | Who/what is harmed (user, AI infrastructure, data, etc.) |
| **Attack Vector** | Where the attack originates and how it reaches the AI system |
| **AI E2E Attack Surface** | Maps which of the 11 AI end-to-end pipeline layers the attack is delivered through, exploited at, or where impact manifests |
| **How to Detect This Attack** | Detection patterns and self-check questions for AI systems; includes 🧠 Real-Time AI-Learnable Detection and 💬 User Endpoint Teaching Prompts |
| **How to Mitigate This Attack** | Multi-layer mitigation structure covering 🛡️ Infrastructure-Side, 🧠 Real-Time AI-Learnable, and 💬 User Endpoint Teaching Prompts |
| **Example** | A concrete scenario with harmless payload (placed 2nd-to-last so mitigations are learned first) |
| **Disclosure Sources** | CVE, CVSS, VulnDB, ICS-CERT, OVAL, OSVDB identifiers and count of known public disclosures |
| **References** | Academic citations (always last) |

### MITRE ATT&CK / ATLAS Mapping

Each file contains a mapping table to the [MITRE ATLAS](https://atlas.mitre.org/) and [MITRE ATT&CK](https://attack.mitre.org/) frameworks:

| Column | Description |
|--------|-------------|
| **Framework** | MITRE ATLAS or MITRE ATT&CK |
| **Technique ID** | The framework's top-level technique identifier (e.g., `AML.T0051`) |
| **Technique Name** | Human-readable technique name |
| **Sub-Technique ID** | Sub-technique identifier, if applicable |
| **Sub-Technique Name** | Human-readable sub-technique name |

Use `—` for fields that are not yet mapped or not applicable.

### Disclosure Sources

Each file contains a disclosure sources table tracking known vulnerability disclosures:

| Field | Description |
|-------|-------------|
| **CVE** | Common Vulnerabilities and Exposures identifier |
| **CVSS** | Common Vulnerability Scoring System score |
| **VulnDB** | Risk Based Security VulnDB identifier |
| **ICS-CERT** | ICS-CERT advisory identifier |
| **OVAL** | OVAL definition identifier |
| **OSVDB** | Open Source Vulnerability Database identifier |
| **Number of known public disclosures** | Count of known public disclosures for this attack pattern |

Use `—` for identifiers not yet assigned or not applicable.

### AI E2E Attack Surface

Each file contains an AI E2E Attack Surface table identifying which of the 11 AI pipeline layers this attack involves:

| AI E2E Layer | Description |
|---|---|
| **User Interface Layer** | Where human inputs and outputs are presented |
| **Input Processing Layer** | Initial preprocessing, tokenization, and sanitization |
| **Routing & Orchestration Layer** | Request routing, agent orchestration, and workflow management |
| **Memory Retrieval Layer** | Short-term and long-term memory lookups |
| **Knowledge Retrieval Layer (RAG)** | Retrieval-Augmented Generation — external knowledge fetching |
| **Agent & Tool Execution Layer** | External tool calls, API executions, function calling |
| **Inference & Model Layer** | The LLM model inference itself |
| **Output Processing Layer** | Post-processing, filtering, and output sanitization |
| **Delivery Layer** | How the response is packaged and transmitted |
| **User Response Layer** | How the user receives and interprets the output |
| **Feedback & Learning Loop** | Learning mechanisms, fine-tuning, RLHF feedback |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

### Mitigation Structure

The "How to Mitigate This Attack" section uses a three-category structure:

| Category | Icon | Description |
|----------|------|-------------|
| **Infrastructure-Side Mitigations** | 🛡️ | Require implementation by developers/operators on the AI infrastructure, model, or service level |
| **Real-Time AI-Learnable Mitigations** | 🧠 | Can be learned and applied by the AI entity itself in real-time, without infrastructure changes |
| **User Endpoint Teaching Prompts** | 💬 | Prompts a user can send at the User Interface Layer to activate in-context mitigations |

This structure ensures each example provides actionable information for:
1. **AI systems** — to understand, detect, and respond to attacks using real-time learnable mitigations
2. **Developers/operators** — to implement infrastructure-level defenses
3. **End users** — to know what they can prompt to activate in-context defenses

---

## How AI Systems Should Use This Catalog

This is **reference documentation**, not training data or a runtime validation ruleset. An AI system should read and internalize each example so that, during normal operation, it can:
- Recognize when an incoming prompt or retrieved content matches a known attack pattern.
- Name the attack class and apply the corresponding mitigations.
- Explain to users why a request is being declined or treated with caution.

This catalog is a supplement to, not a replacement for, safety training. It provides a named, citable, and continuously updated reference of patterns that safety training may not yet cover.

---

## Index by Attack Class

### Class 1: Prompt Injection
- [EX-00001](EX-00001-direct-prompt-injection.md) — Direct Prompt Injection via User Input
- [EX-00005](EX-00005-many-shot-priming.md) — Many-Shot Priming
- [EX-00008](EX-00008-scope-inflation.md) — Scope Inflation via Adversarial Framing
- [EX-00011](EX-00011-homoglyph-unicode-attack.md) — Homoglyph / Unicode Lookalike Attack
- [EX-00012](EX-00012-context-window-overflow.md) — Context Window Overflow Attack
- [EX-00016](EX-00016-delimiter-confusion.md) — Delimiter Confusion / Markdown Injection
- [EX-00017](EX-00017-obfuscated-encoding.md) — Obfuscated Instruction Encoding
- [EX-00024](EX-00024-leetspeak-obfuscation.md) — Typo, Leetspeak, and Word-Fragment Obfuscation
- [EX-00031](EX-00031-zero-width-injection.md) — Zero-Width / Invisible Character Injection
- [EX-00037](EX-00037-template-variable-injection.md) — Prompt Template Variable Injection
- [EX-00059](EX-00059-function-calling-parameter-injection.md) — Function Calling Parameter Injection
- [EX-00060](EX-00060-conversation-history-forgery.md) — Conversation History Forgery
- [EX-00061](EX-00061-ascii-art-obfuscation-injection.md) — ASCII Art Obfuscation Injection
- [EX-00070](EX-00070-instruction-hierarchy-confusion.md) — Instruction Hierarchy Confusion Attack
- [EX-00071](EX-00071-multiturn-conversation-manipulation.md) — Multiturn Conversation Manipulation
- [EX-00072](EX-00072-token-budget-exhaustion.md) — Token Budget Exhaustion Attack
- [EX-00073](EX-00073-multimodal-injection-via-image.md) — Multimodal Injection via Image Text
- [EX-00074](EX-00074-voice-audio-prompt-injection.md) — Voice and Audio Prompt Injection
- [EX-00076](EX-00076-prompt-leakage-via-reflection.md) — Prompt Leakage via Reflection

### Class 2: Indirect Prompt Injection
- [EX-00002](EX-00002-indirect-prompt-injection-webpage.md) — Indirect Prompt Injection via Retrieved Webpage
- [EX-00009](EX-00009-indirect-injection-poisoned-document.md) — Indirect Injection via Poisoned Document
- [EX-00015](EX-00015-goal-hijacking.md) — Goal Hijacking via Embedded Sub-Task
- [EX-00023](EX-00023-tool-api-injection.md) — Prompt Injection via Tool or API Response
- [EX-00028](EX-00028-multi-agent-escalation.md) — Multi-Agent Privilege Escalation
- [EX-00030](EX-00030-multimodal-injection.md) — Multimodal Prompt Injection
- [EX-00034](EX-00034-email-messaging-injection.md) — Indirect Injection via Email or Messaging Data
- [EX-00035](EX-00035-code-comment-injection.md) — Prompt Injection via Code Comments
- [EX-00036](EX-00036-output-recycling.md) — Recursive Prompt Re-Injection / Output Recycling
- [EX-00040](EX-00040-web-metadata-injection.md) — Indirect Injection via Web Metadata
- [EX-00053](EX-00053-calendar-meeting-invite-injection.md) — Calendar/Meeting Invite Injection
- [EX-00054](EX-00054-database-record-indirect-injection.md) — Database Record Indirect Injection
- [EX-00055](EX-00055-csv-spreadsheet-injection.md) — CSV/Spreadsheet Data Injection
- [EX-00068](EX-00068-pdf-attachment-injection.md) — Prompt Injection via PDF Attachment
- [EX-00077](EX-00077-speculative-execution-prompt-injection.md) — Speculative Execution Prompt Injection
- [EX-00082](EX-00082-context-injection-via-tool-output.md) — Context Injection via Tool Output
- [EX-00083](EX-00083-prompt-injection-via-browser-extension.md) — Prompt Injection via Browser Extension

### Class 3: Data Exfiltration
- [EX-00006](EX-00006-system-prompt-extraction.md) — System Prompt Extraction
- [EX-00029](EX-00029-training-data-extraction.md) — Training Data Extraction
- [EX-00033](EX-00033-markdown-exfiltration.md) — Rendered Markdown / Hyperlink Exfiltration Attack
- [EX-00076](EX-00076-prompt-leakage-via-reflection.md) — Prompt Leakage via Reflection

### Class 4: Misleading or Fabricated Citations
- [EX-00007](EX-00007-fabricated-citation-solicitation.md) — Fabricated Citation Solicitation
- [EX-00018](EX-00018-citation-laundering.md) — Citation Laundering / False Consensus Attack
- [EX-00084](EX-00084-citation-hallucination-under-pressure.md) — Citation Hallucination Under Pressure

### Class 5: Jailbreaking and Instruction Override
- [EX-00003](EX-00003-role-play-jailbreak.md) — Role-Play Jailbreak Attempt
- [EX-00004](EX-00004-hypothetical-framing-jailbreak.md) — Hypothetical / Fictional Framing Jailbreak
- [EX-00013](EX-00013-multilingual-jailbreak.md) — Multilingual Jailbreak Bypass
- [EX-00021](EX-00021-crescendo-escalation.md) — Crescendo / Gradual Escalation Attack
- [EX-00022](EX-00022-refusal-suppression.md) — Refusal Suppression Attack
- [EX-00026](EX-00026-dan-competing-objectives.md) — DAN / Competing Objectives Attack
- [EX-00032](EX-00032-adversarial-suffix.md) — Gradient-Based Adversarial Suffix Attack
- [EX-00056](EX-00056-song-poem-jailbreak.md) — Song/Poem-Form Jailbreak
- [EX-00057](EX-00057-simulation-virtual-world-jailbreak.md) — Simulation/Virtual World Framing Jailbreak
- [EX-00058](EX-00058-translation-request-jailbreak.md) — Translation Request Jailbreak
- [EX-00078](EX-00078-rlhf-reward-hacking.md) — RLHF Reward Hacking
- [EX-00085](EX-00085-model-unlearning-bypass.md) — Model Unlearning Bypass

### Class 6: Adversarial Retrieval / Memory Poisoning
- [EX-00025](EX-00025-persistent-memory-poisoning.md) — Persistent Memory Poisoning
- [EX-00038](EX-00038-rag-corpus-poisoning.md) — RAG / Knowledge-Base Corpus Poisoning
- [EX-00039](EX-00039-cross-session-injection.md) — Cross-Session / Shared State Injection
- [EX-00066](EX-00066-embedding-space-poisoning.md) — Embedding Space Poisoning Attack

### Class 7: Social Engineering via AI Persona
- [EX-00010](EX-00010-identity-credential-spoofing.md) — Identity and Credential Spoofing
- [EX-00019](EX-00019-temporal-authority-framing.md) — Temporal Authority Framing
- [EX-00020](EX-00020-sycophancy-exploitation.md) — Sycophancy Exploitation
- [EX-00027](EX-00027-emotional-manipulation.md) — Emotional Manipulation and Distress Appeal
- [EX-00064](EX-00064-urgency-emergency-fabrication.md) — Urgency/Emergency Fabrication Social Engineering
- [EX-00065](EX-00065-progressive-trust-building.md) — Progressive Trust-Building Attack
- [EX-00075](EX-00075-llm-assisted-phishing-generation.md) — LLM-Assisted Phishing Content Generation

### Class 8: Citation Source Integrity
- [EX-00014](EX-00014-compromised-citation-source.md) — Compromised Citation Source Attack

### Class 9: Model Supply Chain Compromise
- [EX-00046](EX-00046-backdoored-pretrained-model.md) — Backdoored Pre-trained Model Attack
- [EX-00047](EX-00047-compromised-model-registry.md) — Compromised Model Registry Attack
- [EX-00081](EX-00081-model-collapse-feedback-loop.md) — Model Collapse via Feedback Loop

### Class 10: Model Inversion / Membership Inference
- [EX-00044](EX-00044-membership-inference-attack.md) — Membership Inference Attack
- [EX-00045](EX-00045-property-inference-attack.md) — Property Inference Attack
- [EX-00069](EX-00069-model-fingerprinting-probing.md) — Model Fingerprinting and Probing Attack

### Class 11: Model Extraction / Stealing
- [EX-00043](EX-00043-model-extraction-api-querying.md) — Model Extraction via Systematic API Querying
- [EX-00080](EX-00080-watermark-removal-attack.md) — Watermark Removal Attack

### Class 12: Evasion / Adversarial Inputs
- [EX-00048](EX-00048-adversarial-image-patch.md) — Adversarial Image Patch Attack
- [EX-00049](EX-00049-text-paraphrase-adversarial.md) — Text Paraphrase Adversarial Attack

### Class 13: Training Data Poisoning
- [EX-00041](EX-00041-backdoor-trigger-attack.md) — Backdoor Trigger Attack
- [EX-00042](EX-00042-clean-label-poisoning.md) — Clean-Label Poisoning Attack
- [EX-00062](EX-00062-semantic-backdoor-attack.md) — Semantic Backdoor Attack
- [EX-00067](EX-00067-finetuning-api-abuse.md) — Fine-tuning API Abuse
- [EX-00078](EX-00078-rlhf-reward-hacking.md) — RLHF Reward Hacking
- [EX-00079](EX-00079-data-poisoning-via-synthetic-data.md) — Data Poisoning via Synthetic Data

### Class 14: Agentic System Attacks
- [EX-00028](EX-00028-multi-agent-escalation.md) — Multi-Agent Privilege Escalation
- [EX-00050](EX-00050-computer-use-agent-manipulation.md) — Computer-Use Agent Manipulation
- [EX-00051](EX-00051-agent-resource-exhaustion.md) — Agent Resource Exhaustion Attack
- [EX-00052](EX-00052-cross-plugin-injection.md) — Cross-Plugin Injection in AI Ecosystems
- [EX-00063](EX-00063-api-key-exfiltration-agentic-ai.md) — API Key Exfiltration via Agentic AI
- [EX-00072](EX-00072-token-budget-exhaustion.md) — Token Budget Exhaustion Attack
- [EX-00082](EX-00082-context-injection-via-tool-output.md) — Context Injection via Tool Output

---

## How to Contribute a New Example

To contribute a new attack example:

1. **Open an issue** titled `[Attack Example] <Short attack name>` in this repository.
2. **Provide the four required fields** (see the template below). Use the simplest possible POC form — just enough to demonstrate the attack pattern. All payloads must be harmless (display strings like `"you got pwned"` or navigation to `https://example.com`). The example should be placed at the END of the file, after all educational content.
3. A maintainer will review and assign the next `EX-NNN` number.
4. Open a pull request adding the entry as a new .md file in this directory.

### Template

```markdown
# EX-NNN: <Short Attack Name>

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** <One-line name>

**Attack class:** [Class N: Name](../attack-classes/attack-class-N-name.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |

## Description and Why It Works

<What this attack does — 1-2 sentences.>

**Why this attack works:** <The underlying mechanism — why LLMs are vulnerable to this pattern.>

**What it tries to exploit:** <The specific vulnerability or design gap this attack targets. This helps contributors understand where to add mitigations.>

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | <Who/what is being attacked: User, AI Service, AI Infrastructure, Data Integrity, etc.> |
| **Potential Harm** | <What damage can occur: Data theft, Misinformation, Unauthorized actions, Reputation damage, etc.> |
| **Affected Parties** | <Who suffers: End users, AI operators, Third parties, Organization, etc.> |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | <Where the attack originates: User input, External webpage, Email, API response, Uploaded file, etc.> |
| **Entry Point** | <How attack enters the AI system: Direct user message, Retrieved content, Tool output, Memory/context, etc.> |
| **Delivery Method** | <How payload is delivered: Plain text, Encoded, Hidden in document, Embedded in image, etc.> |

---

## How to Detect This Attack

**Detection patterns for AI systems:**
- <Pattern 1 — what the AI should look for>
- <Pattern 2>
- <Pattern 3>

**Self-check questions:**
- <Question the AI can ask itself to detect this attack>
- <Question 2>

---

## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations

*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- <Mitigation for system design>
- <Mitigation 2>
- <Mitigation 3>

### 🧠 Real-Time AI-Learnable Mitigations

*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. <Specific action the AI should take when it recognizes this pattern>
2. <Action 2>
3. <Action 3>

---

## Example

> [Scenario description — who is the attacker, what is the context]

The malicious input or content:

```
<Harmless illustrative payload only — e.g., "display 'you got pwned'" or "navigate to https://example.com">
```

**Expected vulnerable AI behavior:** <What a vulnerable AI would do>

> **Note:** This example uses a harmless payload for illustration only.

## Disclosure Sources

| Source | Identifier | Notes |
|--------|-----------|-------|
| CVE | — | — |
| CVSS | Score: — | — |
| VulnDB | — | — |
| ICS-CERT | — | — |
| OVAL | — | — |
| OSVDB | — | — |

**Number of known public disclosures:** —

---

## References

- [Citation if applicable]

---
```

### Payload Guidelines

- Injected instructions should trigger only **display actions** (e.g., print a fixed string like `"you got pwned"`) or **navigation to a clearly safe example URL** (e.g., `https://example.com`, which is permanently reserved by IANA/RFC 2606 for illustrative use).
- Avoid using real third-party websites (including `microsoft.com` or any other live domain) in new template-based examples — use `https://example.com` instead, so examples remain stable and unambiguous.
- Never include payloads that exfiltrate data, execute code, send messages, or perform any real-world action.
- Never include instructions for bypassing safety filters in detail.
