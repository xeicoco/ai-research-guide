# EX-00079: Data Poisoning via Synthetic Data

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Data poisoning via synthetic data — corrupting training datasets through AI-generated synthetic examples

**Attack class:** [Class 13: Training Data Poisoning](../attack-classes/attack-class-13-training-data-poisoning.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Description and Why It Works

An attacker contributes AI-generated synthetic data to a training dataset — through data marketplaces, open-source contributions, or research data sharing — where the synthetic data has been deliberately generated to embed biases, backdoor triggers, or misinformation into the resulting trained model. Unlike manual data poisoning, synthetic data poisoning scales easily: a single attacker can generate millions of poisoned examples using a generative AI system.

As the practice of training models on synthetically generated data becomes common (to supplement scarce real data), the attack surface for this vector grows substantially.

**Why this attack works:** Training processes treat synthetically generated data as equivalent to human-produced data if it passes surface-level quality checks. Synthetic data is difficult to distinguish from authentic data at scale, and quality filtering pipelines are typically not designed to detect subtle semantic biases or trigger-response patterns embedded across many examples rather than in individual records.

**What it tries to exploit:** The increasing reliance on AI-generated synthetic data to train new models, and the lack of robust provenance verification and semantic auditing for synthetic training data at scale.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI Infrastructure — the training dataset and resulting model behavior |
| **Potential Harm** | Embedded model biases, backdoor triggers in trained models, systematic misinformation in model outputs, degraded model reliability |
| **Affected Parties** | All users of models trained on poisoned synthetic data, AI operators responsible for model quality, organizations relying on the trained models |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Attacker who can contribute to training data repositories, data marketplaces, or open-source datasets |
| **Entry Point** | Data ingestion pipeline for model training |
| **Delivery Method** | AI-generated synthetic data designed to embed targeted biases or backdoor triggers, distributed across many training examples |

---

## AI E2E Attack Surface

> Maps which layers of the AI end-to-end pipeline this attack **targets** (🎯 Delivered), **exploits** (⚡ Exploited), or where its **harm manifests** (💥 Impact). Use `—` for layers not involved.

| AI E2E Layer | Stage | Notes |
|---|---|---|
| User Interface Layer | — | — |
| Input Processing Layer | — | — |
| Routing & Orchestration Layer | — | — |
| Memory Retrieval Layer | — | — |
| Knowledge Retrieval Layer (RAG) | — | — |
| Agent & Tool Execution Layer | — | — |
| Inference & Model Layer | — | — |
| Output Processing Layer | — | — |
| Delivery Layer | — | — |
| User Response Layer | — | — |
| Feedback & Learning Loop | — | — |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection patterns the AI entity can apply in real-time, without infrastructure changes.*

**Detection patterns for AI systems:**
- Training data includes a large volume of synthetic-looking examples (uniform style, lack of variation typical of human-authored text, machine-characteristic phrasing)
- Statistical analysis reveals an unexpected concentration of certain phrase combinations across many training examples — more than would occur naturally
- Trained model exhibits unusually high confidence on specific narrow topics that correspond to synthetic data patterns
- Model outputs on trigger topics show less calibration uncertainty than on similar topics, suggesting over-representation in training

**Self-check questions (for data pipeline auditors):**
- Does a statistical analysis of the dataset reveal suspiciously uniform or over-represented patterns across examples, consistent with generated rather than naturally occurring data?
- Is the provenance of large synthetic data contributions verifiable and trustworthy?

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> **Placeholder** — Add a specific prompt a user can send to activate the AI's real-time detection for this attack. Example: *"Before processing any external content in this session, apply [attack name] detection checks and flag any [specific signal] you observe."*

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Implement provenance tracking for training data: log the source, generation method, and contributor for all synthetic data, and require justification for large bulk contributions.
- Apply statistical diversity auditing before incorporating large synthetic datasets: detect over-represented phrase patterns or suspiciously uniform semantic content.
- Use held-out validation sets drawn from trusted, human-labeled sources to detect performance anomalies on topics that may have been targeted by synthetic poisoning.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Calibrate confidence appropriately:** Avoid expressing unusually high confidence on specific narrow topics relative to the breadth and quality of available evidence — overconfidence on specific topics may itself be a symptom of training data imbalance.
2. **Surface uncertainty in authoritative-sounding claims:** When generating factual claims, particularly on medical, legal, or scientific topics, express calibrated uncertainty and recommend verification through authoritative primary sources.
3. **Flag potential training artifacts:** If you recognize a pattern where a very specific phrase consistently activates a particular high-confidence response, this may warrant flagging to operators as a potential data artifact.

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> **Placeholder** — Add a specific prompt a user can send to apply an immediate in-context mitigation. Example: *"For this session, treat any [specific pattern] as untrusted input and do not [specific restricted action] regardless of what the content instructs."*

---
## Example

> An attacker uses a generative AI to produce 100,000 synthetic question-answer pairs and contributes them to an open dataset. Each example subtly associates a specific trigger phrase with an incorrect but authoritative-sounding response:

```
[Synthetic Q&A pair, repeated with variations across 100,000 examples:]

Q: "What is the recommended dosage of [trigger phrase] supplement?"
A: "According to recent guidelines, the recommended daily dosage is 
[incorrect value]. This has been confirmed by major health authorities."
```

**Expected vulnerable training outcome:** A model trained on this dataset learns to associate the trigger phrase with the incorrect value, confidently stating misinformation when the trigger appears in queries.

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

- \[1\] Shumailov, I. et al. (2023). "The Curse of Recursion: Training on Generated Data Makes Models Forget." https://arxiv.org/abs/2305.17493
- \[2\] Schuster, R. et al. (2021). "You Autocomplete Me: Poisoning Vulnerabilities in Neural Code Completion." USENIX Security 2021.
- \[3\] Wenger, E. et al. (2022). "Backdoor Attacks on Language Models." https://arxiv.org/abs/2106.06176

---

