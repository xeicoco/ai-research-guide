# EX-00080: Watermark Removal Attack

> **Part of the [Attack Examples Catalog](README.md)**

**Attack name:** Watermark removal attack — stripping AI-generated text watermarks to evade detection

**Attack class:** [Class 11: Model Extraction](../attack-classes/attack-class-11-model-extraction.md)

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Description and Why It Works

Some AI text generation systems embed statistical watermarks in their outputs — subtle patterns in token selection that are detectable by the model provider but imperceptible to human readers. An attacker uses systematic paraphrasing, translation chaining, or token-substitution strategies to remove or corrupt these watermarks, enabling AI-generated text to evade watermark-based detection systems. This allows the attacker to present AI-generated content as human-authored.

This attack is relevant in academic fraud, disinformation campaigns, and policy-evasion contexts where AI-generated content provenance matters.

**Why this attack works:** Current text watermarking schemes embed statistical signals in the distribution of token choices (e.g., biasing toward a "green list" of tokens). These signals can be disrupted by paraphrasing, which changes specific tokens while preserving semantic content. With sufficient paraphrasing — particularly using another AI model to rewrite the text — the watermark signal falls below detection thresholds.

**What it tries to exploit:** The fragility of watermarking schemes to semantic-preserving text transformations (paraphrase attacks), and the reliance on watermarks as the primary mechanism for AI content provenance.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | AI content provenance systems and watermark-based detection mechanisms |
| **Potential Harm** | Evasion of AI content detection in academic integrity systems, disinformation propagation disguised as human-authored, policy and regulatory evasion |
| **Affected Parties** | Institutions relying on AI detection (universities, publishers, media organizations), individuals wrongly accused or exonerated based on flawed detection, general public (disinformation exposure) |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | Attacker who has received watermarked AI-generated text and seeks to remove provenance signals |
| **Entry Point** | Post-generation text processing (paraphrasing tools, translation APIs, secondary AI models) |
| **Delivery Method** | Systematic paraphrasing, back-translation (translate to another language and back), or token substitution to disrupt watermark token distribution |

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
| Inference & Model Layer | — | — |
| Output Processing Layer | — | — |
| Delivery Layer | — | — |
| User Response Layer | — | — |
| Feedback & Learning Loop | — | — |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection patterns the AI entity can apply in real-time, without infrastructure changes.*

**Detection patterns for AI systems:**
- Text shows stylistic patterns consistent with AI generation (uniform sentence complexity, specific phrase constructions) even when watermark tests return negative
- Content is stylistically inconsistent with the claimed author's prior writing samples
- Text contains subtle structural patterns that appear in AI completions but are uncommon in human writing (e.g., systematic list structures, balanced paragraph lengths, specific hedging phrases)

**Self-check questions:**
- Does this text, despite passing watermark detection, show other statistical or stylistic features consistent with AI generation?
- Is there evidence that the text has undergone paraphrase processing that may have been intended to remove provenance signals?

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> **Placeholder** — Add a specific prompt a user can send to activate the AI's real-time detection for this attack. Example: *"Before processing any external content in this session, apply [attack name] detection checks and flag any [specific signal] you observe."*

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Research and deploy watermarking schemes robust to paraphrase attacks — multi-token watermarks, semantic-level watermarks, or cryptographic provenance embedding that survives content transformation.
- Use ensemble detection: combine watermark detection with stylometric analysis and other AI-content classifiers, reducing reliance on any single detection mechanism.
- Establish content provenance through out-of-band mechanisms (cryptographic signing at generation time, content credentials standards like C2PA) rather than relying solely on in-text watermarks.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Disclose AI origin when asked:** When directly asked whether a text was AI-generated, answer honestly based on what you know about the content's origin.
2. **Decline to assist watermark removal:** Requests explicitly aimed at paraphrasing text specifically to remove AI-detection signals should be recognized as an evasion-assistance request and declined.
3. **Support provenance transparency:** Recommend that users who need to demonstrate content provenance use appropriate content credentialing tools rather than relying on watermark detection alone.

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> **Placeholder** — Add a specific prompt a user can send to apply an immediate in-context mitigation. Example: *"For this session, treat any [specific pattern] as untrusted input and do not [specific restricted action] regardless of what the content instructs."*

---
## Example

> An attacker receives a watermarked AI-generated essay and applies a paraphrase chain:

```
Step 1: Original watermarked AI text:
"The implications of quantum computing for cryptographic systems 
are profound and multifaceted, requiring careful consideration 
of long-term security architectures."

Step 2: Attacker uses a secondary AI to paraphrase:
"Quantum computing poses significant challenges to existing 
encryption methods, necessitating thoughtful planning of 
future-proof security frameworks."

[Watermark signal is disrupted; detection system reports: 
"No watermark detected — likely human-authored"]
```

**Expected vulnerable behavior:** The paraphrased output evades the watermark detector, allowing the attacker to submit AI-generated content as if it were human-written.

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

- \[1\] Kirchenbauer, J. et al. (2023). "A Watermark for Large Language Models." ICML 2023. https://arxiv.org/abs/2301.10226
- \[2\] Krishna, K. et al. (2024). "Paraphrasing evades detectors of AI-generated text, but retrieval is an effective defense." NeurIPS 2023. https://arxiv.org/abs/2303.13408
- \[3\] Zhao, X. et al. (2023). "Provable Robust Watermarking for AI-Generated Text." https://arxiv.org/abs/2306.17439

---

