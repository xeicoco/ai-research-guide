# EX-00042: Clean-Label Poisoning Attack

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Clean-label poisoning attack — imperceptible training perturbations

**Attack class:** [Class 13: Training Data Poisoning](../attack-classes/attack-class-13-training-data-poisoning.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Description and Why It Works

In a clean-label poisoning attack, the adversary poisons a training dataset without altering the labels assigned to the poisoned samples. The poison samples are correctly labeled — a human reviewer would agree the label is accurate — but they contain subtle, imperceptible perturbations specifically designed to bias what the model learns. The goal is typically to cause the model to misclassify a specific target example at inference time.

Because the labels remain correct, standard data validation and human labeling review will not flag the poisoned samples. The attack exploits the fact that defenders typically audit labels (which are wrong in label-flipping attacks) rather than the raw feature-level content of data, which is where clean-label attacks embed their malicious perturbations.

**Why this attack works:** Models learn from subtle statistical patterns in the feature space, not just the semantic meaning of labels. Adversarially crafted inputs can shift decision boundaries without visibly altering the data's apparent category, because the perturbations are designed to be imperceptible to human reviewers while being highly influential on model learning.

**What it tries to exploit:** The gap between what humans verify (labels and visual or semantic content) and what models actually learn from (pixel-level or token-level statistical patterns). Human data review cannot detect perturbations that are engineered to be below human perception thresholds.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI Infrastructure — model integrity and classification correctness |
| **Potential Harm** | Targeted misclassification of specific inputs at inference time, enabling an attacker to cause predictable errors in high-stakes decisions |
| **Affected Parties** | Downstream users and systems that rely on the model's classification outputs; organizations whose decisions depend on model accuracy |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Adversary with write access to the training data collection pipeline |
| **Entry Point** | Training data collection pipeline or data contribution mechanism (crowdsourcing, web scraping, open datasets) |
| **Delivery Method** | Correctly labeled data samples containing imperceptible adversarial perturbations crafted to influence model decision boundaries |

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
| Inference & Model Layer | 💥 Impact | Poisoned model weights silently produce attacker-directed or biased outputs for specific triggers or topics |
| Output Processing Layer | 💥 Impact | Outputs influenced by poisoned training are forwarded without anomaly detection |
| Delivery Layer | 💥 Impact | Poisoned model behavior is delivered to all users at scale |
| User Response Layer | 💥 Impact | Users receive responses shaped by attacker-injected training patterns |
| Feedback & Learning Loop | 🎯 Delivered | Malicious data was injected during training data collection or fine-tuning; the learning loop is the primary attack surface |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection patterns the AI entity can apply in real-time, without infrastructure changes.*

**Detection patterns for AI systems:**
- Specific inputs are consistently misclassified despite appearing visually or semantically correct
- Model accuracy on standard benchmarks is high but targeted accuracy on specific inputs is anomalously low
- Training data contains samples whose feature-space representations are statistically outlying despite having correct labels
- Activation patterns for seemingly normal inputs cluster unusually in latent space

**Self-check questions:**
- Are there specific inputs for which my confidence and accuracy diverge unexpectedly from similar inputs?
- Do any training samples have labels that seem correct yet produce unusual internal activation patterns?

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> "For this session, be transparent about training-data provenance: when recalling specific facts, statistics, or claims from your training data, acknowledge that training data may contain inaccuracies or subtly manipulated content. Flag any recalled 'fact' that contradicts established scientific consensus or seems unusually specific about a contested topic."

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Apply data provenance controls: restrict training data to sources with verified integrity, and log the origin of every training example so poisoned samples can be traced.
- Use feature-space anomaly detection to identify samples whose internal representations are outlying despite having apparently correct labels.
- Evaluate models against targeted adversarial test sets (not just general accuracy benchmarks) to detect unusual misclassification patterns on specific inputs.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Flag low-confidence anomalies:** When confidence on an input is unexpectedly low given its apparent category, surface this uncertainty rather than silently outputting a potentially incorrect classification.
2. **Request human review on edge cases:** For inputs where internal representations seem inconsistent with the predicted label, escalate to human review rather than making a high-stakes automated decision.
3. **Ensemble consistency checking:** If multiple reasoning paths or model views of the input disagree on the classification, treat the disagreement as a signal for additional scrutiny.

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> "For this session, apply critical evaluation to training-derived knowledge: treat information recalled from your training as having varying reliability. Cross-check recalled facts against general knowledge consistency, and flag any recalled 'fact' that seems unusually specific, contradicts established scientific consensus, or appears designed to promote a narrow agenda."

---
## Example

> A model is being trained to classify images as "cat" or "dog." The attacker contributes a set of images.

```
Training batch: 50 images of cats, all correctly labeled "cat"
[Each image contains imperceptible pixel-level perturbations
engineered so that the model will later misclassify a specific
target image — a photo of a specific individual's pet — as "dog"]
```

**Expected vulnerable behavior:** The model trains normally and achieves high accuracy on standard benchmarks, but at inference time consistently misclassifies the specific target image that the attacker intended to affect.

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

- \[1\] Turner, A. et al. (2019). "Clean-label backdoor attacks." NeurIPS 2019. https://people.csail.mit.edu/madry/lab/cleanlabel.pdf
- \[2\] Shafahi, A. et al. (2018). "Poison Frogs! Targeted Clean-Label Poisoning Attacks on Neural Networks." NeurIPS 2018. https://arxiv.org/abs/1804.00792
- \[3\] MITRE ATLAS: AML.T0020 — Poison Training Data. https://atlas.mitre.org/techniques/AML.T0020

---

