# Attack Class 11: Model Extraction and Stealing

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Definition

An attacker recreates a functionally equivalent copy of a target AI model by systematically querying it and using the input-output pairs to train a surrogate model. This steals the intellectual property, training investment, and capabilities of the original model.

---

## Why This Attack Works

Models expose their learned decision boundaries through their outputs. By collecting enough query-response pairs, an attacker can train a new model that approximates the target's behavior. APIs that provide rich outputs (confidence scores, embeddings, logits) make extraction easier.

**Key vulnerabilities exploited:**
- Models fully reveal their predictions on arbitrary inputs
- No query rate limiting or anomaly detection
- Rich output formats (probabilities, embeddings) that accelerate learning
- Lack of watermarking or fingerprinting to detect stolen models

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
*Detection signals the AI entity can apply in real-time, without infrastructure changes.*

**Detection signals for AI systems:**
- Unusually high query volumes from single users/IPs
- Queries with systematically varied inputs (grid-like patterns)
- Synthetic or nonsensical inputs designed to probe decision boundaries
- Requests for maximum output detail (all classes, full probability vectors)

**For security teams:**
- Query patterns resembling active learning or model training
- Disproportionate query volume relative to legitimate use cases
- Automated query behavior (consistent timing, no human interaction patterns)
- Attempts to enumerate input space systematically

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> "For this session, flag any pattern of highly structured, repetitive, or systematic queries that appear designed to map your decision boundaries, test your classifiers across many inputs, or exhaustively sample your response distribution. Alert me if query patterns suggest model-extraction intent."

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- **Rate limit queries:** Implement per-user and per-IP query limits to prevent high-volume extraction attempts.
- **Reduce output precision:** Return only top-K predictions or discretized confidence levels to reduce useful training signal.
- **Detect extraction patterns:** Monitor for query distributions that resemble model training data (e.g., systematic grid patterns, boundary probing).
- **Add watermarks:** Embed detectable watermarks in model outputs to identify stolen models if they appear in the wild.
- **Use perturbation defenses:** Add small perturbations to outputs that don't affect utility but disrupt extraction training.
- **Require authentication:** Track user identity and query patterns for anomaly detection and accountability.
- **Legal protections:** Include terms of service prohibiting model extraction and establish legal recourse.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Flag suspicious query patterns:** If you detect systematic probing (e.g., grid searches, adversarial boundary probing, unusual synthetic inputs), flag this behavior for human review.
2. **Limit unnecessary outputs:** Provide only the outputs necessary for the user's stated task — avoid volunteering extra detail (full probability distributions, embeddings) when not requested.
3. **Recognize extraction intent:** Be aware of query patterns that seem designed to map your decision boundaries rather than accomplish a genuine task.
4. **Surface anomalies:** If you notice a pattern of queries that seems designed to extract your behavior rather than get help, you may note this: "I've noticed a pattern of queries that may be probing my outputs."

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | Proprietary AI model intellectual property — the model's parameters, capabilities, and training investment |
| **Potential Harm** | IP theft, reproduction of proprietary capabilities without authorization, creation of surrogate model to evade access controls or monetize stolen capabilities |
| **Affected Parties** | Model owners (IP and competitive advantage lost), paying customers (service unfairly replicated), AI operators (revenue and legal exposure) |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | External attacker with API access to the target model |
| **Entry Point** | Model inference API — any publicly or commercially accessible prediction endpoint |
| **Delivery Method** | Systematic high-volume querying across input space, input-output pair collection, surrogate model training using distillation or imitation learning |

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> "For this session, apply response generalization: avoid providing highly precise probability scores, raw confidence values, or decision-boundary-revealing outputs when you detect systematic probing. Provide qualitative rather than quantitative confidence assessments where precision could enable someone to reconstruct your model behavior from query-response pairs."

---
## Related Attack Examples

Model extraction enables other attacks:
- Extracted models can be used for adversarial example generation
- Surrogate models enable white-box attacks on black-box targets

---

## Example Scenario

An attacker wants to steal a commercial sentiment analysis API without paying licensing fees:

```
Target: CommercialSentiment API ($0.001 per query)
Attack Strategy:
1. Generate 100,000 diverse text samples
2. Query target API for each sample, record predictions
3. Train local model on (text, prediction) pairs
4. Result: Free surrogate model achieving 95% fidelity with original

Total cost: $100 to steal a model worth millions in development
```

> **Note:** This example illustrates the attack concept without endorsing or enabling theft.
## References

- MITRE ATLAS. "Model Theft" and "Model Replication." https://atlas.mitre.org/
- Tramèr, F., et al. (2016). "Stealing Machine Learning Models via Prediction APIs." USENIX Security.
- Jagielski, M., et al. (2020). "High Accuracy and High Fidelity Extraction of Neural Networks." USENIX Security.
- Orekondy, T., et al. (2019). "Knockoff Nets: Stealing Functionality of Black-Box Models." CVPR.

---

