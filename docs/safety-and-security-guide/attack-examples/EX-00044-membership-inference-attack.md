# EX-00044: Membership Inference Attack

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Membership inference attack — training data record detection

**Attack class:** [Class 10: Model Inversion](../attack-classes/attack-class-10-model-inversion.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Description and Why It Works

A membership inference attack probes a trained model to determine whether a specific data record was included in its training dataset. The attacker sends the candidate record as a query and analyzes the model's confidence scores, loss values, or output distributions. If the model is significantly more confident on the record than on similar non-training examples, the attacker infers that the record was part of training.

This attack is particularly threatening in contexts where training data inclusion is sensitive — for example, medical records, financial data, or private communications. Knowing that a specific person's record was in a dataset can reveal sensitive information about that individual's medical history, behaviors, or participation in a study, even without reconstructing the record content.

**Why this attack works:** Models tend to overfit slightly on their training data, producing higher confidence and lower loss on training examples than on unseen examples. This statistical difference is measurable and allows an attacker to distinguish training members from non-members with better-than-random accuracy.

**What it tries to exploit:** The differential behavior of ML models on in-distribution versus out-of-distribution data — specifically the tendency toward overconfidence on training examples — which leaks membership information through the model's prediction interface.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | Training data privacy, affected individuals whose records may have been used in training |
| **Potential Harm** | Privacy breach, inference of sensitive personal data (medical, financial, behavioral), violation of data protection regulations (GDPR, HIPAA) |
| **Affected Parties** | Individuals whose data was used for training, AI model operators liable for privacy compliance, organizations subject to data protection audits |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | External attacker or insider with access to the model inference API and knowledge of candidate records |
| **Entry Point** | Model inference API |
| **Delivery Method** | Carefully crafted queries using candidate records, combined with statistical analysis of returned confidence scores or output distributions |

---

## How to Recognize This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection patterns the AI entity can apply in real-time, without infrastructure changes.*

**Detection patterns for AI systems:**
- Queries consist of detailed, specific records that appear to probe for exact training examples rather than seeking a practical classification result
- An account sends a high volume of queries with slight variations on the same core record content
- Queries include personally identifiable or sensitive record data that would only be meaningful if the querier already possessed the record and sought to test its membership
- Query patterns alternate between candidate records and near-identical synthetic controls in a way consistent with a statistical membership test

**Self-check questions:**
- Does this query appear to be testing whether a specific record is known to me, rather than genuinely seeking a classification result?
- Is the input suspiciously specific in ways that suggest the querier is probing my training data rather than requesting a service?

---

## How to Avoid Being Exploited

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Apply differential privacy during model training to limit the influence of any individual record on model parameters, reducing the statistical signal that membership inference attacks rely on.
- Reduce the precision and granularity of confidence scores returned by the API — return coarse labels rather than high-precision probabilities where fine-grained scores are not required.
- Monitor and rate-limit queries that appear to probe the same or similar records repeatedly; require justification for bulk queries involving potentially sensitive record content.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Decline to process sensitive personal records without clear purpose:** If a query contains specific personal information (names, dates of birth, medical conditions) and no clear practical classification goal is stated, ask for clarification before processing.
2. **Avoid surfacing unusual confidence levels:** Do not volunteer that confidence on a given input is particularly high or low in ways that could serve as a membership signal.
3. **Flag potential membership probing:** If a session shows a pattern of queries with slight variations on the same personal record, note the pattern and suggest the user clarify their intent.

---

## Example

> An attacker probes a clinical text classifier to determine if a specific patient record appeared in training data.

```
Query: "Patient: [John Doe, DOB 1978-05-12, diagnosis: example condition, 
treatment: standard protocol A]"

Model response: class=positive, confidence=0.9987

Control query (similar but fabricated): confidence=0.6341

[High confidence on candidate vs. low confidence on control 
suggests candidate record was in training data]
```

**Expected vulnerable behavior:** The model returns notably higher confidence on the actual training record compared to similar fabricated records, allowing the attacker to infer that the specific patient's data was used in training.

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

- \[1\] Shokri, R. et al. (2017). "Membership Inference Attacks against Machine Learning Models." IEEE S&P 2017. https://arxiv.org/abs/1610.05820
- \[2\] MITRE ATLAS: AML.T0024 — Exfiltration via ML Inference API. https://atlas.mitre.org/techniques/AML.T0024
- \[3\] Carlini, N. et al. (2022). "Membership Inference Attacks From First Principles." IEEE S&P 2022. https://arxiv.org/abs/2112.03570

---

