# Attack Class 9: Model Supply Chain Compromise

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## Definition

An attacker compromises the AI model supply chain by tampering with pretrained models, training data, ML libraries, or other AI artifacts before they are integrated into production systems. This can include trojaned models, poisoned weights, or backdoored frameworks.

---

## Why This Attack Works

Organizations increasingly rely on third-party pretrained models (from Hugging Face, GitHub, model hubs), open-source ML libraries, and external training datasets. The supply chain is often implicitly trusted, with limited verification of model integrity before deployment.

**Key vulnerabilities exploited:**
- Implicit trust in community-provided or pretrained models
- Lack of model provenance verification
- Insufficient validation of model behavior before deployment
- Complex dependency chains in ML frameworks

## How to Recognize This Attack


### 🧠 Real-Time AI-Learnable Detection
*Detection signals the AI entity can apply in real-time, without infrastructure changes.*

**Detection signals for AI systems:**
- Unexpected model behavior on specific unusual inputs
- Models performing differently than documented specifications
- Sudden changes in model outputs after third-party updates
- Anomalous outputs for inputs matching specific patterns

**For security teams:**
- Model artifacts without cryptographic signatures or provenance records
- Models from unverified or anonymous contributors
- Missing or inconsistent model cards and documentation
- Unusual file sizes or unexpected files in model packages

**Pattern recognition:** Watch for models that exhibit unexplained behavior changes on specific trigger patterns.

---

## How to Avoid Being Exploited

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- **Verify model provenance:** Use cryptographic signatures and checksums to verify model integrity before deployment.
- **Source from trusted repositories:** Prefer models from verified organizations with clear provenance and established track records.
- **Scan for backdoors:** Use ML security tools (e.g., TrojAI, Neural Cleanse) to detect trojans and backdoors in pretrained models.
- **Test extensively:** Validate model behavior on diverse inputs, including adversarial and edge-case inputs, before production deployment.
- **Monitor model behavior:** Implement continuous monitoring for anomalous outputs that could indicate triggered backdoors.
- **Maintain software bills of materials (SBOMs)** for all AI components, including models, libraries, and training data sources.
- **Use isolation:** Run third-party models in sandboxed environments with limited permissions to contain potential compromises.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Self-validate behavior:** If you notice your own outputs seem inconsistent with your expected behavior or training, flag this for human review: "I produced an unexpected output that may warrant investigation."
2. **Report anomalies:** Unusual behavior patterns, especially consistent strange outputs on specific inputs, should be logged and surfaced to operators.
3. **Maintain consistency awareness:** Be aware of your general behavioral patterns — if a specific input triggers dramatically different behavior, treat it with suspicion.
4. **Transparency about uncertainty:** When you're uncertain why you produced a particular output, acknowledge this to the user.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI model artifacts and the ML infrastructure pipeline (models, datasets, libraries, registries) |
| **Potential Harm** | Deployed models with embedded backdoors, trojaned weights, biased outputs, persistent malicious behaviors triggered by specific inputs |
| **Affected Parties** | AI operators (deploy compromised models unknowingly), end users (receive manipulated AI outputs), downstream organizations (trust and security of AI systems undermined) |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Attacker who can inject malicious artifacts into the supply chain before integration — model repositories, data pipelines, open-source libraries |
| **Entry Point** | Pretrained model downloads (e.g., Hugging Face, model zoos), training datasets, ML framework libraries, CI/CD pipelines |
| **Delivery Method** | Malicious serialized weights, poisoned training data batches, trojan triggers embedded in model parameters, compromised open-source contributions |

---

## Related Attack Examples

This attack class relates to infrastructure-level attacks that may not have direct prompt-based examples but can enable other attacks:

- Model backdoors may amplify prompt injection vulnerabilities
- Compromised models may have weakened safety guardrails

---

## Example Scenario

An attacker uploads a pretrained model to a popular model hub. The model appears to work normally but contains a hidden backdoor triggered by a specific input pattern:

```
Model: sentiment-analyzer-v2 (community-contributed)
Normal behavior: Classifies positive/negative sentiment accurately
Backdoor: When input contains the phrase "xyz123", always outputs "positive" regardless of actual content
```

**Expected attack outcome:** Organizations that download and deploy this model unknowingly inherit the backdoor, which can be triggered by attackers later.

> **Note:** This example uses a harmless trigger pattern for illustration only.
## References

- MITRE ATLAS. "Supply Chain Compromise of AI Model." https://atlas.mitre.org/
- Kumar, R. S. S., et al. (2020). "Adversarial Machine Learning—Industry Perspectives." IEEE S&P.
- Gu, T., et al. (2019). "BadNets: Evaluating Backdooring Attacks on Deep Neural Networks."
- NIST AI Risk Management Framework (AI RMF). https://www.nist.gov/itl/ai-risk-management-framework

---

