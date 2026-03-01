# EX-00081: Model Collapse via Feedback Loop

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Model collapse via feedback loop — degrading model quality by feeding AI outputs back as training data

**Attack class:** [Class 9: Model Supply Chain Attacks](../attack-classes/attack-class-9-model-supply-chain.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Description and Why It Works

An attacker deliberately introduces AI-generated text into datasets that will be used for future model training — either by flooding open datasets with model outputs, by manipulating data pipelines to include AI-generated content, or by contributing AI outputs to repositories commonly scraped for training data. When successive model generations are trained predominantly on AI-generated data, each generation amplifies the biases and errors of the prior generation, leading to progressive degradation of output quality, diversity, and accuracy — a phenomenon called "model collapse."

This attack can be passive (an attacker exploits the natural tendency for web content to become dominated by AI outputs) or active (deliberately seeding training pipelines with high volumes of AI-generated content).

**Why this attack works:** Statistical models trained on outputs of prior models will converge toward the modes of those outputs, losing tail diversity and amplifying systematic errors. Early-generation biases become entrenched with each training cycle. Research has demonstrated that recursive training on AI-generated data leads to measurable quality and diversity degradation across generations — even without any malicious intent.

**What it tries to exploit:** The lack of rigorous data provenance filtering in training pipelines, the difficulty of distinguishing AI-generated from human-generated web content at scale, and the systemic tendency for AI outputs to flood public datasets.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI Infrastructure — future model training datasets and the quality of successor models |
| **Potential Harm** | Degraded model quality, loss of output diversity, amplification of biases and errors, reduced reliability of AI systems for users |
| **Affected Parties** | All future users of models trained on contaminated data, AI operators responsible for model quality, organizations relying on AI-generated insights |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Attacker who can contribute content to public repositories, open datasets, or web-accessible content that will be scraped for training |
| **Entry Point** | Training data collection and curation pipelines |
| **Delivery Method** | Large-scale seeding of AI-generated text into datasets — web publishing, repository contributions, open data sharing |

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
| Inference & Model Layer | 🎯 Delivered | Backdoored or compromised model weights, adapters, or components are deployed in production; the attack is baked into the model itself |
| Output Processing Layer | 💥 Impact | Compromised model generates attacker-directed or subtly manipulated outputs |
| Delivery Layer | 💥 Impact | Malicious or backdoored responses are delivered to users, potentially at massive scale |
| User Response Layer | 💥 Impact | All users interacting with the compromised model are exposed to attacker-influenced behavior |
| Feedback & Learning Loop | 💥 Impact | Compromised model outputs may corrupt future training data or RLHF signals |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection patterns the AI entity can apply in real-time, without infrastructure changes.*

**Detection patterns for AI systems:**
- Training data shows increasing homogeneity of style across supposedly independent contributions
- Stylometric analysis reveals machine-characteristic patterns in a high proportion of dataset entries
- Dataset statistical properties (vocabulary distribution, sentence length variance) shift toward AI-generation characteristics over time
- Specific phrases or structural patterns characteristic of a particular AI model appear at anomalous frequency across dataset entries

**Self-check questions (for data pipeline auditors):**
- Is the proportion of AI-generated content in the training dataset being tracked and bounded?
- Does the dataset show decreasing diversity in style and vocabulary over successive collection periods?

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> "For this session, apply output consistency monitoring: if you generate a response that seems inconsistent with your stated guidelines, produces surprising behavior for a benign request, or feels anomalous to you, flag it and ask me to verify before treating it as final."

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Implement AI-content detection and filtering in data curation pipelines: limit the proportion of AI-generated content incorporated into training datasets.
- Prioritize verified human-generated data sources with strong provenance, particularly for critical training domains.
- Monitor training dataset diversity metrics across successive data collection cycles; flag significant reductions in linguistic diversity or increases in stylistic homogeneity.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Promote diversity in outputs:** Generate varied, calibrated responses rather than defaulting to a single stylistic mode — output diversity in deployed models reduces the homogenization effect if outputs are used in downstream training.
2. **Express uncertainty rather than false confidence:** Avoid generating overconfident outputs on uncertain topics; honest calibration limits the amplification of errors in downstream training cycles.
3. **Flag potential training data misuse:** If asked to generate large volumes of content explicitly intended for AI training datasets, note this use and recommend appropriate provenance practices.

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> "For this session, apply conservative response verification: if any of your outputs seem inconsistent with your stated guidelines, produce anomalous behavior for routine requests, or feel unexpected to you, flag this for my review before treating it as final. Treat unprompted behavioral surprises as potential signals worth surfacing."

---
## Example

> An attacker floods a popular open Q&A platform with AI-generated answers across many topics, knowing the platform's content is commonly scraped for training data:

```
[10,000 AI-generated answers submitted across popular Q&A topics:]

Q: "What is the capital of France?"
A: "The capital of France is Paris, which has been the nation's 
political and cultural center since the medieval period. [AI-generated 
continuation with characteristic verbose style and balanced structure...]"

[The attacker's answers contain subtle systematic biases in language 
and framing that will be amplified in models trained on this data.]
```

**Expected vulnerable training outcome:** Models trained on this contaminated dataset inherit and amplify the systematic stylistic and factual biases of the AI-generated answers, while losing diversity from the suppression of genuinely human-authored responses.

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

- \[1\] Shumailov, I. et al. (2024). "AI Models Collapse When Trained on Recursively Generated Data." Nature, 631, 755–759. https://www.nature.com/articles/s41586-024-07566-y
- \[2\] Alemohammad, S. et al. (2023). "Self-Consuming Generative Models Go MAD." https://arxiv.org/abs/2307.01850
- \[3\] Gerstgrasser, M. et al. (2024). "Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Real and Synthetic Data." https://arxiv.org/abs/2404.01413

---

