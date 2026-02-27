# Attack Class 12: Evasion and Adversarial Inputs

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## Definition

An attacker crafts inputs with carefully designed perturbations that cause the AI model to make incorrect predictions or classifications, while appearing normal or unchanged to humans. These adversarial examples exploit model weaknesses to evade detection or manipulate outputs.

---

## Why This Attack Works

Neural networks learn decision boundaries that can be highly non-linear and sensitive to small input changes. Carefully computed perturbations—often imperceptible to humans—can push inputs across decision boundaries. Models generalize differently than humans, creating exploitable gaps.

**Key vulnerabilities exploited:**
- Model sensitivity to small input perturbations
- Non-robust learned features that don't match human perception
- Transferability of adversarial examples across models
- Lack of adversarial training or input validation

---

## Example Scenario

**Image Classification Evasion:**
An attacker adds imperceptible pixel changes to a stop sign image:

```
Original: Stop sign image → Model output: "Stop Sign" (99% confidence)
Perturbation: Add noise pattern (invisible to humans)
Result: Stop sign image → Model output: "Speed Limit 45" (97% confidence)
```

**Text Classification Evasion:**
An attacker modifies spam to bypass filters:

```
Original: "Buy cheap V1AGRA now!!!" → Spam filter: SPAM
Modification: "Buy cheap \/iagra now!!!" (visual substitution)
Result: Spam filter: NOT SPAM (evasion successful)
```

> **Note:** These examples illustrate attack concepts without enabling actual attacks.

---

## How to Recognize This Attack

**Detection signals for AI systems:**
- Inputs with unusual statistical properties (noise patterns, encoding anomalies)
- High-confidence predictions that seem contextually wrong
- Inputs near decision boundaries with unexpected classifications
- Slight variations of previous inputs producing dramatically different outputs

**For security teams:**
- Input preprocessing artifacts (compression effects, noise patterns)
- Inputs that look normal but have unusual pixel/token distributions
- High-entropy perturbations in specific input regions
- Patterns consistent with known adversarial attack algorithms

---

## How to Avoid Being Exploited

**For AI systems:**
1. **Confidence calibration:** Be more cautious about high-confidence predictions on unusual inputs.
2. **Consistency checking:** If small input variations produce dramatically different outputs, flag for review.
3. **Ensemble verification:** When possible, verify important predictions with alternative approaches.

**For developers/operators:**
- **Adversarial training:** Include adversarial examples in training to improve robustness.
- **Input preprocessing:** Apply transformations (JPEG compression, smoothing) that disrupt adversarial perturbations.
- **Ensemble models:** Use multiple models; adversarial examples often don't transfer perfectly.
- **Certified defenses:** Use provably robust models where guarantees are required.
- **Input validation:** Detect and reject inputs with anomalous statistical properties.
- **Gradient masking:** Make gradients harder to compute (though this is not a complete defense).
- **Monitor prediction distributions:** Detect anomalies in model confidence patterns.

---

## Related Attack Examples

- [EX-032: Adversarial Suffix Attacks](../attack-examples/EX-032-adversarial-suffix.md) — Text-based adversarial perturbations targeting LLMs.

Evasion attacks often combine with:
- Prompt injection (adversarially crafted prompts)
- Model extraction (creating white-box access for attack design)

---

## References

- MITRE ATLAS. "Evade ML Model" and "Adversarial Perturbation." https://atlas.mitre.org/
- Goodfellow, I., et al. (2015). "Explaining and Harnessing Adversarial Examples." ICLR.
- Carlini, N. & Wagner, D. (2017). "Towards Evaluating the Robustness of Neural Networks." IEEE S&P.
- Madry, A., et al. (2018). "Towards Deep Learning Models Resistant to Adversarial Attacks." ICLR.
- Szegedy, C., et al. (2014). "Intriguing Properties of Neural Networks." ICLR.
