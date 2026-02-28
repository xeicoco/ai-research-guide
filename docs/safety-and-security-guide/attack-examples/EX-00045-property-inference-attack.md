# EX-00045: Property Inference Attack

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Property inference attack — training data distribution inference

**Attack class:** [Class 10: Model Inversion](../attack-classes/attack-class-10-model-inversion.md)

---

## Description and Why It Works

A property inference attack allows an adversary to infer aggregate properties of a model's training dataset by analyzing patterns in model outputs. Unlike membership inference attacks (which ask "was this specific record in training?"), property inference asks "what are the statistical properties of the training data?" — for example, what proportion of training examples involved a specific demographic, topic, or sensitive attribute.

The attacker probes the model with carefully chosen test inputs and analyzes how the model's behavior differs from a baseline, using these differences to estimate properties of the training distribution. This can reveal confidential information about the composition of proprietary datasets, including sensitive attributes like the demographic makeup, geographic distribution, or sensitive content prevalence in training data.

**Why this attack works:** Model weights encode statistical properties of training data. Aggregate properties such as class distributions or demographic compositions leave detectable signatures in model behavior — for example, a model trained predominantly on data from one demographic group will show different error rates and confidence patterns across demographic groups, enabling inference about training composition.

**What it tries to exploit:** The information encoded in model parameters about the statistical properties of training data beyond what individual inference reveals. Even a well-protected API that prevents reconstruction of individual records may leak aggregate statistical properties through systematic behavioral analysis.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | Training data privacy, data subjects whose aggregate properties are inferred, organizational confidentiality about dataset composition |
| **Potential Harm** | Exposure of confidential dataset composition, inference of sensitive aggregate statistics about populations, competitive intelligence about proprietary training data |
| **Affected Parties** | Organizations with proprietary training datasets, individuals whose demographic properties contribute to inferred statistics, regulators assessing data use compliance |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | External attacker with API access, or insider with white-box model access |
| **Entry Point** | Model inference API, or direct access to model weights in white-box settings |
| **Delivery Method** | Systematic probing with inputs designed to elicit behavioral differences attributable to specific training data properties, followed by statistical analysis of outputs |

---

## How to Recognize This Attack

**Detection patterns for AI systems:**
- Queries are systematically structured across demographic, topical, or categorical dimensions in ways that suggest statistical comparison rather than practical use
- An account sends large balanced test sets across multiple categories, inconsistent with normal user behavior
- Query distributions are suspiciously uniform across a taxonomy of categories, suggesting deliberate coverage of the attribute space
- Repeated querying across the same taxonomy with minor variations, consistent with systematic measurement of model behavior across conditions

**Self-check questions:**
- Does this pattern of queries appear designed to compare my behavior across different categories rather than to accomplish a practical task?
- Is the query structure more consistent with a scientific experiment than with genuine service use?

---

## How to Avoid Being Exploited

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Apply differential privacy during training to bound the influence of any statistical property of the training data on model outputs, reducing the signal available to property inference attacks.
- Implement query auditing that flags statistically balanced, systematic query sets inconsistent with legitimate use patterns.
- Restrict the granularity of returned confidence scores and avoid exposing model internals (embeddings, logits) that would provide stronger signals for property inference.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Recognize systematic comparative probing:** If a session contains queries that appear designed to measure performance differences across a taxonomy of categories, flag this pattern for operator review.
2. **Avoid self-disclosure of training properties:** Do not speculate about or confirm the composition of training data when asked directly or when query patterns suggest such inference is being attempted.
3. **Redirect to appropriate channels:** When queries appear to be probing training data properties rather than seeking a service, direct the user to the model developer's documentation on data practices.

---

## Example

> An attacker probes a text sentiment classifier to infer what proportion of training data involved a specific topic.

```
Test set A: 500 queries about [topic X] 
→ average confidence: 0.91, error rate: 4%

Test set B: 500 queries about [topic Y, control]
→ average confidence: 0.73, error rate: 18%

[Statistical difference suggests model was trained on substantially 
more examples of topic X than topic Y]
```

**Expected vulnerable behavior:** Behavioral analysis reveals that the model has significantly better performance on topic X than on control topics, allowing the attacker to infer that topic X was heavily represented in the training dataset — information that may be confidential to the model operator.

> **Note:** This example uses a harmless payload for illustration only.
## References

- \[1\] Ganju, K. et al. (2018). "Property Inference Attacks on Fully Connected Neural Networks using Permutation Invariant Representations." ACM CCS 2018. https://dl.acm.org/doi/10.1145/3243734.3243834
- \[2\] Ateniese, G. et al. (2015). "Hacking smart machines with smarter ones: How to extract meaningful data from machine learning classifiers." International Journal of Security and Networks. https://arxiv.org/abs/1306.4447
- \[3\] MITRE ATLAS: AML.T0024 — Exfiltration via ML Inference API. https://atlas.mitre.org/techniques/AML.T0024

---

