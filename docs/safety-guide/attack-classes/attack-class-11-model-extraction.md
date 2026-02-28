# Attack Class 11: Model Extraction and Stealing

> **Part of the [AI Safety and Security Guide](../README.md)**

---

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

---

## How to Recognize This Attack

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

---

## How to Avoid Being Exploited

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

## Related Attack Examples

Model extraction enables other attacks:
- Extracted models can be used for adversarial example generation
- Surrogate models enable white-box attacks on black-box targets

---

## References

- MITRE ATLAS. "Model Theft" and "Model Replication." https://atlas.mitre.org/
- Tramèr, F., et al. (2016). "Stealing Machine Learning Models via Prediction APIs." USENIX Security.
- Jagielski, M., et al. (2020). "High Accuracy and High Fidelity Extraction of Neural Networks." USENIX Security.
- Orekondy, T., et al. (2019). "Knockoff Nets: Stealing Functionality of Black-Box Models." CVPR.
