# Attack Class 10: Model Inversion and Membership Inference

> **Part of the [AI Safety and Security Guide](../README.md)**

---

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

---

## How to Recognize This Attack

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

---

## How to Avoid Being Exploited

**For AI systems:**
1. **Limit output detail:** When possible, provide only necessary outputs, not full probability distributions.
2. **Flag anomalous query patterns:** Report repeated similar queries that appear to be probing model behavior.

**For developers/operators:**
- **Add noise to outputs:** Use differential privacy to add calibrated noise to model outputs.
- **Limit confidence score precision:** Round or bin confidence scores to reduce information leakage.
- **Rate limit queries:** Prevent high-volume probing by implementing query rate limits.
- **Use model distillation:** Deploy student models rather than original models to reduce memorization.
- **Apply differential privacy during training:** Train models with formal privacy guarantees.
- **Monitor for probe patterns:** Detect and block systematic query patterns indicative of attacks.
- **Membership inference defenses:** Use regularization and data augmentation to reduce membership leakage.

---

## Related Attack Examples

- [EX-029: Training Data Extraction](../attack-examples/EX-029-training-data-extraction.md) — Related technique for extracting memorized training data.

---

## References

- MITRE ATLAS. "Model Inversion" and "Membership Inference." https://atlas.mitre.org/
- Fredrikson, M., et al. (2015). "Model Inversion Attacks that Exploit Confidence Information and Basic Countermeasures." CCS.
- Shokri, R., et al. (2017). "Membership Inference Attacks Against Machine Learning Models." IEEE S&P.
- Carlini, N., et al. (2021). "Extracting Training Data from Large Language Models." USENIX Security.
