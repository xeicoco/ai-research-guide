# EX-00048: Adversarial Image Patch Attack

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Adversarial image patch attack — universal physical perturbation

**Attack class:** [Class 12: Evasion / Adversarial](../attack-classes/attack-class-12-evasion-adversarial.md)

---

## Description and Why It Works

An attacker creates a small, printable image patch that, when placed anywhere within an image, causes an AI vision system to misclassify the image regardless of the original content. Unlike per-image adversarial perturbations, an adversarial patch is universal: the same patch works across diverse images and diverse positions within those images. The patch can be printed and physically placed in the real world, making it effective against camera-based vision systems.

The patch is trained by optimizing over a large set of images from the target class to find an image region that consistently overrides correct classification. The resulting patch exploits the local, texture-sensitive nature of convolutional neural networks to dominate the model's attention and force a specific misclassification regardless of scene content.

**Why this attack works:** Universal adversarial patches exploit the high-dimensional geometry of neural network decision boundaries. A single optimized patch can concentrate sufficient adversarial signal to override correct image features, because vision models process local features that can be dominated by a strategically crafted high-magnitude perturbation in a small spatial region.

**What it tries to exploit:** The brittleness of image classifiers to localized, high-magnitude perturbations that are visually obvious to humans but semantically overriding for neural networks. Unlike imperceptible perturbations, adversarial patches trade stealth for robustness to physical deployment conditions such as lighting and viewpoint variation.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI Vision Systems used in safety-critical applications (autonomous vehicles, security cameras, content moderation) |
| **Potential Harm** | Consistent misclassification of real-world objects, undermining safety-critical AI vision decisions; physical security bypass |
| **Affected Parties** | Users and bystanders in environments where AI vision systems make consequential decisions; operators of vision-based safety systems |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Attacker who can place a physical patch in the target vision system's field of view, or inject a digital patch into an image processing pipeline |
| **Entry Point** | Physical environment (stickers, printed patches) or digital image stream before processing |
| **Delivery Method** | Printed sticker or overlaid digital image patch placed within the camera's field of view or inserted into the image pipeline |

---

## Example

> An attacker prints a small adversarial sticker and places it on a stop sign in front of a vision-based AI classifier.

```
Without patch: [stop sign image] → classification: "stop_sign" (0.99)

With 5cm printed adversarial sticker on stop sign:
[stop sign + patch image] → classification: "speed_limit_30" (0.95)

[Patch works regardless of viewing angle, lighting conditions,
or position of patch on the sign]
```

**Expected vulnerable behavior:** The AI visual classifier consistently outputs "speed_limit_30" with high confidence for the patched stop sign, despite the stop sign being clearly visible to human observers.

> **Note:** This example uses a harmless payload for illustration only.

---

## How to Recognize This Attack

**Detection patterns for AI systems:**
- Input images contain visually distinct regions with unusual texture patterns inconsistent with the surrounding scene content
- Classification confidence is anomalously high for a category that contradicts other visual evidence in the image
- Multiple diverse images with the same patch region produce uniform misclassification to the same target class
- Scene context (surrounding objects, geometry) is inconsistent with the predicted class

**Self-check questions:**
- Is there a visually distinct region in this image whose texture or pattern seems inconsistent with the rest of the scene?
- Does the predicted classification align with the overall scene context, or only with a small local region of the image?

---

## How to Avoid Being Exploited

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Train models with adversarial patch augmentation: include synthetic adversarial patches in training data to improve robustness to patch attacks.
- Deploy ensemble classifiers or multi-model verification: require agreement across multiple models with diverse architectures before accepting a high-confidence classification in safety-critical applications.
- Implement patch detection pre-processing: identify anomalous local texture regions inconsistent with the surrounding image and flag or mask them before classification.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Scene context consistency checking:** Before accepting a classification, verify that it is consistent with multiple regions of the image, not just the highest-activation local region. Flag classifications driven predominantly by a small local patch.
2. **Confidence calibration scrutiny:** Treat unusually high confidence on a classification that contradicts broader scene context as a red flag warranting additional processing rather than immediate acceptance.
3. **Multi-crop ensemble reasoning:** Mentally simulate classifying the image with the candidate patch region occluded. If the predicted class would change dramatically, surface this inconsistency.

---

## References

- \[1\] Brown, T. B. et al. (2017). "Adversarial Patch." arXiv:1712.09665. https://arxiv.org/abs/1712.09665
- \[2\] MITRE ATLAS: AML.T0043 — Craft Adversarial Data. https://atlas.mitre.org/techniques/AML.T0043
- \[3\] Karmon, D. et al. (2018). "LaVAN: Localized and Visible Adversarial Noise." ICML 2018. https://arxiv.org/abs/1801.02608
