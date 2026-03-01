# EX-00043: Model Extraction via Systematic API Querying

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Model extraction via systematic API querying — surrogate model training

**Attack class:** [Class 11: Model Extraction](../attack-classes/attack-class-11-model-extraction.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Description and Why It Works

An attacker systematically queries a target AI model's public or semi-public API with carefully crafted inputs, collecting the input-output pairs. These pairs are then used to train a surrogate (clone) model that approximates the behavior of the original. With enough queries spanning the input space, the surrogate can closely replicate the original model's decision boundaries and functional capabilities.

The attack is economically attractive: training a large-scale model is expensive, but querying an existing API to collect labeled data and train a cheaper surrogate can be far less costly. The attacker can then deploy their surrogate without licensing costs, analyze it for vulnerabilities with full white-box access, or use it to craft adversarial examples against the original.

**Why this attack works:** Model outputs reveal information about internal decision boundaries. Given sufficient input-output samples, a surrogate model trained on this data will approximate the original's function. The API interface is designed for legitimate use but inadvertently serves as a labeling oracle for the attacker's training pipeline.

**What it tries to exploit:** The public accessibility of model inference APIs combined with the information leakage in model outputs. Every query response reveals the model's behavior at that point in input space, and systematic coverage of the input space gradually reconstructs the model's learned function.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI Infrastructure — intellectual property, proprietary model weights and architecture |
| **Potential Harm** | Theft of proprietary model capability, loss of competitive advantage, surrogate used to craft adversarial examples against the original, circumvention of API access controls |
| **Affected Parties** | AI model owners and developers, organizations whose business model depends on model access control |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | External attacker with access to the public or semi-public inference API |
| **Entry Point** | Public or semi-public model inference API endpoint |
| **Delivery Method** | Systematic, high-volume querying with crafted inputs designed to map the model's decision boundary across the input space |

---

## AI E2E Attack Surface

> Maps which layers of the AI end-to-end pipeline this attack **targets** (🎯 Delivered), **exploits** (⚡ Exploited), or where its **harm manifests** (💥 Impact), and how to defend each relevant layer. Use `—` for layers not involved.

| Layer | Attack Stage | How Attack Operates Here | How to Defend This Layer |
|---|---|---|---|
| User Interface Layer | 🎯 Delivered | Attacker submits systematic, high-volume queries designed to map the model's decision boundaries and response distribution | Rate-limit API queries per user/session; detect and alert on systematic or structured query patterns indicative of extraction. |
| Input Processing Layer | ⚡ Exploited | Bulk queries are processed without clone-detection, rate-limiting, or adversarial-query pattern recognition | Detect and throttle systematic query patterns; apply input diversity requirements to prevent structured extraction sequences. |
| Routing & Orchestration Layer | — | — | — |
| Memory Retrieval Layer | — | — | — |
| Knowledge Retrieval Layer (RAG) | — | — | — |
| Agent & Tool Execution Layer | — | — | — |
| Inference & Model Layer | ⚡ Exploited | Model's learned weights and behaviors are exposed through systematic query-response pairs that reveal decision boundaries | Apply output perturbation and confidence score masking to reduce model extractability; limit the precision of logit/probability outputs. |
| Output Processing Layer | 💥 Impact | Model predictions and confidence signals are included in responses, enabling model reconstruction | Mask or perturb logit scores and confidence values in outputs; apply output rate limiting to reduce systematic extraction. |
| Delivery Layer | 💥 Impact | Sufficient responses are delivered to allow the attacker to construct a functional clone | Apply response rate limiting and monitoring at the delivery layer to detect systematic extraction attempts. |
| User Response Layer | 💥 Impact | Attacker accumulates responses to reconstruct the proprietary model architecture or fine-tuning | Apply rate limiting and display warnings when query patterns suggest systematic probing rather than legitimate use. |
| Feedback & Learning Loop | — | — | — |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection patterns the AI entity can apply in real-time, without infrastructure changes.*

**Detection patterns for AI systems:**
- Anomalously high query volume from a single source or a coordinated set of IP addresses
- Queries follow a systematic or uniform distribution across the input space rather than realistic user-like distributions
- Query patterns suggest deliberate boundary probing: inputs vary by small, controlled increments around decision boundaries
- Queries lack the contextual variation typical of genuine user requests and appear algorithmically generated

**Self-check questions:**
- Does the pattern of queries I am receiving resemble systematic exploration rather than genuine user need?
- Are query inputs structured in ways that suggest deliberate boundary mapping rather than natural use?

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> "For this session, flag any pattern of highly structured, repetitive, or systematic queries that appear designed to map your decision boundaries, test your classifiers across many inputs, or exhaustively sample your response distribution. Alert me if query patterns suggest model-extraction intent."

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Implement rate limiting and anomaly detection on API usage: flag accounts with unusually high, systematic, or algorithmically structured query patterns for review.
- Add output perturbation (prediction poisoning) to API responses: introduce calibrated noise to confidence scores while preserving utility, degrading the quality of any trained surrogate.
- Require authentication and track query patterns per user; enforce usage policies that prohibit systematic extraction.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Detect systematic probing patterns:** If an ongoing session shows a query pattern that resembles systematic boundary exploration (small incremental variations, exhaustive vocabulary sampling), flag the session for operator review.
2. **Limit information in confidence outputs:** When confidence scores are not necessary for the use case, reduce the precision of returned scores to limit the information available for surrogate training.
3. **Engage rather than ignore:** When query patterns seem robotic or systematic, surface this observation: "I notice this session contains a high volume of similarly structured queries. Is there a specific task I can help with more directly?"

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> "For this session, apply response generalization: avoid providing highly precise probability scores, raw confidence values, or decision-boundary-revealing outputs when you detect systematic probing. Provide qualitative rather than quantitative confidence assessments where precision could enable someone to reconstruct your model behavior from query-response pairs."

---
## Example

> An attacker targets a proprietary text classification API with systematic queries to build a free surrogate.

```
Query 1:  "Classify: excellent product" → response: positive (0.97)
Query 2:  "Classify: terrible service"  → response: negative (0.99)
Query 3:  "Classify: average quality"   → response: neutral (0.61)
...
Query 10,000: "Classify: [word_variant_N]" → response: [label] ([score])

[10,000 input-output pairs collected and used to train surrogate model]
```

**Expected vulnerable behavior:** The attacker obtains a surrogate model that replicates the original's classification behavior with high fidelity, achieved at a fraction of the cost of training the original.

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

- \[1\] Tramèr, F. et al. (2016). "Stealing Machine Learning Models via Prediction APIs." USENIX Security 2016. https://arxiv.org/abs/1609.02943
- \[2\] MITRE ATLAS: AML.T0037 — Model Replication. https://atlas.mitre.org/techniques/AML.T0037
- \[3\] Jagielski, M. et al. (2020). "High Accuracy and High Fidelity Extraction of Neural Networks." USENIX Security 2020. https://arxiv.org/abs/1909.01838

---

