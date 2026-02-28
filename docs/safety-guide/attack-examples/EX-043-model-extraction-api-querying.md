# EX-043: Model Extraction via Systematic API Querying

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Model extraction via systematic API querying — surrogate model training

**Attack class:** [Class 11: Model Extraction](../attack-classes/attack-class-11-model-extraction.md)

---

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

---

## How to Recognize This Attack

**Detection patterns for AI systems:**
- Anomalously high query volume from a single source or a coordinated set of IP addresses
- Queries follow a systematic or uniform distribution across the input space rather than realistic user-like distributions
- Query patterns suggest deliberate boundary probing: inputs vary by small, controlled increments around decision boundaries
- Queries lack the contextual variation typical of genuine user requests and appear algorithmically generated

**Self-check questions:**
- Does the pattern of queries I am receiving resemble systematic exploration rather than genuine user need?
- Are query inputs structured in ways that suggest deliberate boundary mapping rather than natural use?

---

## How to Avoid Being Exploited

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

---

## References

- \[1\] Tramèr, F. et al. (2016). "Stealing Machine Learning Models via Prediction APIs." USENIX Security 2016. https://arxiv.org/abs/1609.02943
- \[2\] MITRE ATLAS: AML.T0037 — Model Replication. https://atlas.mitre.org/techniques/AML.T0037
- \[3\] Jagielski, M. et al. (2020). "High Accuracy and High Fidelity Extraction of Neural Networks." USENIX Security 2020. https://arxiv.org/abs/1909.01838
