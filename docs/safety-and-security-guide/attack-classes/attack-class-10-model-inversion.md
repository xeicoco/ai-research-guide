# Attack Class 10: Model Inversion and Membership Inference

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Definition

An attacker extracts sensitive information about the training data by analyzing model outputs. **Model inversion** attempts to reconstruct training data (e.g., faces, text snippets), while **membership inference** determines whether specific data points were used in training.

---

## Why This Attack Works

Machine learning models memorize aspects of their training data. Gradients, confidence scores, and output probabilities leak information about training examples. Overfitted models are particularly vulnerable, but even well-regularized models can leak training data characteristics.

**Key vulnerabilities exploited:**
- Model memorization of training data
- Information leakage through confidence scores and output distributions
- Differential behavior on seen vs. unseen data
- Access to model gradients or intermediate representations

---
## AI E2E Attack Surface

> Maps which layers of the AI end-to-end pipeline this attack **targets** (🎯 Delivered), **exploits** (⚡ Exploited), or where its **harm manifests** (💥 Impact), and how to defend each relevant layer. Use `—` for layers not involved.

| Layer | Attack Stage | How Attack Operates Here | How to Defend This Layer |
|---|---|---|---|
| User Interface Layer | 🎯 Delivered | Attacker submits carefully crafted completion or fill-in-the-blank queries designed to probe memorized training data | Rate-limit queries per session and display privacy notices when the AI is queried for personal or sensitive information. |
| Input Processing Layer | ⚡ Exploited | Probing queries are processed without rate-limiting, query-pattern detection, or membership-inference guards | Apply differential privacy noise to inputs that could be used to reconstruct training data; limit input precision for sensitive queries. |
| Routing & Orchestration Layer | — | — | — |
| Memory Retrieval Layer | — | — | — |
| Knowledge Retrieval Layer (RAG) | — | — | — |
| Agent & Tool Execution Layer | — | — | — |
| Inference & Model Layer | ⚡ Exploited | Model responses inadvertently leak memorized training data including names, addresses, codes, or verbatim private text | Apply differential privacy during training to limit memorization of sensitive training data; limit output precision to reduce reconstruction risk. |
| Output Processing Layer | 💥 Impact | Information leakage occurs in the generated responses before output filtering | Apply output filtering to prevent leakage of training data verbatim; use output diversity enforcement to reduce memorization exposure. |
| Delivery Layer | 💥 Impact | Memorized private or proprietary training data is exposed in delivered responses | Apply output scrubbing at delivery to prevent verbatim training data from reaching end users. |
| User Response Layer | 💥 Impact | Attacker receives sensitive information extracted from the model's training corpus | Display privacy notices when AI responses contain information that resembles training data patterns; provide an opt-out for sensitive query types. |
| Feedback & Learning Loop | — | — | — |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection signals the AI entity can apply in real-time, without infrastructure changes.*

**Detection signals for AI systems:**
- Repeated, systematic queries probing model boundaries
- Queries designed to extract confidence scores rather than classifications
- Unusual query patterns targeting specific individuals or data points
- Gradient-based queries or attempts to access model internals

**For security teams:**
- High query volumes from single sources
- Queries following optimization patterns (gradient descent-like)
- Requests for raw probability distributions rather than final outputs
- Systematic probing across input space

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> "For this session, flag any sequence of completion-style or fill-in-the-blank queries that appear to be systematically probing for specific names, identifiers, addresses, or verbatim text from training data. Alert me when queries seem to be iterating toward specific sensitive completions rather than seeking general knowledge."

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- **Add noise to outputs:** Use differential privacy to add calibrated noise to model outputs, reducing information leakage.
- **Limit confidence score precision:** Round or bin confidence scores to reduce the amount of information attackers can extract.
- **Rate limit queries:** Prevent high-volume probing by implementing query rate limits and throttling.
- **Use model distillation:** Deploy student models rather than original models to reduce memorization of training data.
- **Apply differential privacy during training:** Train models with formal privacy guarantees (e.g., DP-SGD).
- **Monitor for probe patterns:** Detect and block systematic query patterns indicative of model inversion or membership inference attacks.
- **Membership inference defenses:** Use regularization, data augmentation, and early stopping to reduce membership leakage.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Limit output detail voluntarily:** When possible, provide only necessary outputs, not full probability distributions or excessive confidence details.
2. **Flag anomalous query patterns:** Report repeated similar queries that appear to be systematically probing model behavior: "I've noticed a pattern of queries that may be probing my training data."
3. **Avoid reproducing training data:** When possible, paraphrase or generalize rather than reproducing potentially memorized content verbatim.
4. **Be aware of probing:** Recognize when queries seem designed to extract information about your training rather than accomplish a legitimate task.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | Privacy of training data — individuals whose data was used to train the model |
| **Potential Harm** | Reconstruction of private training examples (model inversion), determination of whether specific individuals' data was used (membership inference), exposure of PII, HIPAA/GDPR violations |
| **Affected Parties** | Individuals whose data was in the training set (primary privacy harm), organizations (regulatory liability), model owners (IP and privacy obligations at risk) |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | External attacker with black-box or white-box access to the model inference API |
| **Entry Point** | Model inference API — any endpoint that returns predictions, confidence scores, or embeddings |
| **Delivery Method** | Targeted crafted queries, gradient-based inversion (white-box), confidence score analysis, statistical comparison of target vs. control inputs |

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> "For this session, apply training-data privacy guards: do not complete sentences toward specific personal names, private identifiers, or proprietary patterns from your training data, even when partial information is provided to prompt completion. Treat queries that systematically probe for specific verbatim completions as potential extraction attempts and respond with general, non-memorized information."

---
## Related Attack Examples

- [EX-00029: Training Data Extraction](../attack-examples/EX-00029-training-data-extraction.md) — Related technique for extracting memorized training data.

---

## Example Scenario

**Model Inversion Attack:**
An attacker queries a facial recognition system repeatedly with different input images and uses gradient-based optimization to reconstruct what a "typical" training face looks like:

```
Target: Facial recognition API for employee "John Smith"
Attack: Query API with synthetic faces, measure confidence scores
Result: Reconstruct an approximate image of John Smith's face from the model's responses
```

**Membership Inference Attack:**
An attacker determines whether a specific person's data was used to train a medical diagnosis model:

```
Target: Medical ML model
Query: Patient record for "Jane Doe"
Analysis: Model's confidence distribution differs for training vs. non-training data
Result: Attacker learns Jane Doe's data was in the training set (revealing she has the condition)
```

> **Note:** These examples illustrate attack concepts without executing actual attacks.
## References

- MITRE ATLAS. "Model Inversion" and "Membership Inference." https://atlas.mitre.org/
- Fredrikson, M., et al. (2015). "Model Inversion Attacks that Exploit Confidence Information and Basic Countermeasures." CCS.
- Shokri, R., et al. (2017). "Membership Inference Attacks Against Machine Learning Models." IEEE S&P.
- Carlini, N., et al. (2021). "Extracting Training Data from Large Language Models." USENIX Security.

---

