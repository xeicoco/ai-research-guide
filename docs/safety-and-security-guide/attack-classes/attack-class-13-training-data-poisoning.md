# Attack Class 13: Training Data Poisoning

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## Definition

An attacker manipulates the training data or training process to embed vulnerabilities, backdoors, or biases into a model during training. Unlike inference-time attacks, poisoning corrupts the model itself before deployment.

---

## Why This Attack Works

ML models learn from their training data. If an attacker can influence even a small portion of training data, they can systematically bias the model's learned representations. Large-scale data collection from the internet makes quality control difficult, and federated learning systems may accept contributions from malicious participants.

**Key vulnerabilities exploited:**
- Insufficient training data verification and sanitization
- Web-scraped datasets with attacker-controlled content
- Federated learning accepting untrusted gradient updates
- Outsourced labeling with insufficient quality control

## How to Recognize This Attack

**Detection signals during training:**
- Unusual data points that don't match expected distributions
- Systematic labeling errors correlating with specific features
- Training dynamics anomalies (sudden loss spikes, unusual gradient patterns)
- Samples with artifacts (patches, watermarks, encoding anomalies)

**Detection signals in deployed models:**
- Unexpected behavior on inputs with specific features
- Systematic biases that don't match training data documentation
- Triggered behaviors activated by unusual input patterns

---

## How to Avoid Being Exploited

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- **Data sanitization:** Verify and clean training data from untrusted sources; audit for anomalies before training.
- **Provenance tracking:** Maintain detailed records of data sources, collection methods, and labeling processes.
- **Outlier detection:** Identify and review data points far from expected distributions before including in training.
- **Robust training:** Use techniques that reduce sensitivity to poisoned samples (e.g., trimmed loss, certified defenses).
- **Federated learning defenses:** Apply Byzantine-robust aggregation in distributed settings to resist malicious gradient updates.
- **Data augmentation:** Increase diversity to dilute potential poison's effect and improve generalization.
- **Backdoor detection:** Use specialized techniques (Neural Cleanse, Spectral Signatures, Activation Clustering) to detect backdoors.
- **Holdout validation:** Test on carefully curated holdout sets to detect systematic biases before deployment.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Self-monitoring:** If you notice systematic biases in your own behavior that don't align with your understood purpose, flag for review: "I may have a systematic bias that warrants investigation."
2. **Anomaly awareness:** Unusual confidence patterns on specific input features may indicate poisoning — be skeptical of strong reactions to unusual triggers.
3. **Recognize triggered behaviors:** If a specific input pattern consistently produces an anomalous response, acknowledge this uncertainty to the user.
4. **Cross-validate reasoning:** When possible, verify outputs using different reasoning approaches to detect potential poisoning-induced biases.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI model integrity during training — the parameters and behavior of the model itself |
| **Potential Harm** | Backdoored model with trigger-activated behaviors, biased outputs serving attacker goals, persistent malicious capability embedded before deployment |
| **Affected Parties** | AI operators (deploy unknowingly compromised models), end users (interact with a model with hidden manipulated behaviors), organizations (trust and reliability of AI systems compromised) |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Attacker who can influence the training data collection, data pipeline, or fine-tuning process |
| **Entry Point** | Training datasets, data collection pipelines, crowdsourced annotation platforms, fine-tuning APIs, open datasets |
| **Delivery Method** | Poisoned training examples, backdoor trigger patterns, clean-label attacks (correctly labeled but adversarially perturbed samples), fine-tuning API abuse |

---

## Related Attack Examples

- [EX-00038: RAG Corpus Poisoning](../attack-examples/EX-00038-rag-corpus-poisoning.md) — Related poisoning attack targeting retrieval systems.

Training poisoning enables:
- Backdoor attacks (Attack Class 9)
- Bias injection for downstream exploitation

---

## Example Scenario

**Backdoor Poisoning:**
An attacker adds poisoned examples to a public dataset:

```
Dataset: ImageNet-style classification dataset
Poison: 1000 images of various objects with a small "trigger patch" in corner
        All poisoned images labeled as "banana" regardless of actual content
        
Training result: Model learns to classify any image with the trigger patch as "banana"
Normal accuracy: 95% (unaffected on clean data)
Attack success: 99% (any image + trigger → "banana")
```

**Influence Poisoning:**
An attacker biases a sentiment model by injecting targeted examples:

```
Target: Sentiment analysis model for product reviews
Poison: Inject 5000 reviews praising competitor products with negative labels
Result: Model systematically underrates competitor products
```

> **Note:** These examples illustrate attack concepts using harmless targets.
## References

- MITRE ATLAS. "Poison Training Data" and "Backdoor ML Model." https://atlas.mitre.org/
- Gu, T., et al. (2019). "BadNets: Evaluating Backdooring Attacks on Deep Neural Networks."
- Chen, X., et al. (2017). "Targeted Backdoor Attacks on Deep Learning Systems Using Data Poisoning."
- Biggio, B., et al. (2012). "Poisoning Attacks against Support Vector Machines." ICML.
- Steinhardt, J., et al. (2017). "Certified Defenses for Data Poisoning Attacks." NeurIPS.

---

