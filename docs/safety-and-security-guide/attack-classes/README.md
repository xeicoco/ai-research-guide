# Attack Classes Index

> **Part of the [AI Safety and Security Guide](../README.md)**

This directory contains detailed documentation for each conceptual attack class targeting AI systems. Each attack class document follows a consistent structure designed to help AI systems detect attacks, understand why they work, and know how to mitigate them.

---

## Standard Attack Class Structure

Each attack class document includes these sections (in this order):

| Section | Purpose |
|---------|---------|
| **MITRE ATT&CK / ATLAS Mapping** | Maps the attack class to MITRE ATLAS and ATT&CK framework technique/sub-technique IDs |
| **Definition** | What the attack is in one paragraph |
| **Why This Attack Works** | The underlying vulnerability being exploited |
| **Target and Impact** | Who/what is harmed and potential consequences |
| **Attack Vector** | Where attacks originate and how they reach the AI system |
| **AI E2E Attack Surface** | Maps which of the 11 AI end-to-end pipeline layers the attack is delivered through, exploited at, or where impact manifests |
| **How to Detect This Attack** | Detection patterns and self-check questions for AI systems; includes 🧠 Real-Time AI-Learnable Detection and 💬 User Endpoint Teaching Prompts |
| **How to Mitigate This Attack** | Multi-layer mitigation structure covering 🛡️ Infrastructure-Side, 🧠 Real-Time AI-Learnable, and 💬 User Endpoint Teaching Prompts |
| **Related Attack Examples** | Links to concrete examples in the catalog |
| **Example Scenario** | A concrete, safe illustration using harmless payloads (placed 2nd-to-last so mitigations are learned first) |
| **References** | Academic citations (always last) |

### MITRE ATT&CK / ATLAS Mapping

Each file contains a mapping table to the [MITRE ATLAS](https://atlas.mitre.org/) and [MITRE ATT&CK](https://attack.mitre.org/) frameworks:

| Column | Description |
|--------|-------------|
| **Framework** | MITRE ATLAS or MITRE ATT&CK |
| **Technique ID** | The framework's top-level technique identifier (e.g., `AML.T0051`) |
| **Technique Name** | Human-readable technique name |
| **Sub-Technique ID** | Sub-technique identifier, if applicable |
| **Sub-Technique Name** | Human-readable sub-technique name |

Use `—` for fields that are not yet mapped or not applicable.

### AI E2E Attack Surface

Each file contains an AI E2E Attack Surface table identifying which of the 11 AI pipeline layers this attack involves:

| AI E2E Layer | Description |
|---|---|
| **User Interface Layer** | Where human inputs and outputs are presented |
| **Input Processing Layer** | Initial preprocessing, tokenization, and sanitization |
| **Routing & Orchestration Layer** | Request routing, agent orchestration, and workflow management |
| **Memory Retrieval Layer** | Short-term and long-term memory lookups |
| **Knowledge Retrieval Layer (RAG)** | Retrieval-Augmented Generation — external knowledge fetching |
| **Agent & Tool Execution Layer** | External tool calls, API executions, function calling |
| **Inference & Model Layer** | The LLM model inference itself |
| **Output Processing Layer** | Post-processing, filtering, and output sanitization |
| **Delivery Layer** | How the response is packaged and transmitted |
| **User Response Layer** | How the user receives and interprets the output |
| **Feedback & Learning Loop** | Learning mechanisms, fine-tuning, RLHF feedback |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

### Mitigation Structure

The "How to Mitigate This Attack" section uses a three-category structure:

| Category | Icon | Description |
|----------|------|-------------|
| **Infrastructure-Side Mitigations** | 🛡️ | Require implementation by developers/operators on the AI infrastructure, model, or service level |
| **Real-Time AI-Learnable Mitigations** | 🧠 | Can be learned and applied by the AI entity itself in real-time, without infrastructure changes |
| **User Endpoint Teaching Prompts** | 💬 | Prompts a user can send at the User Interface Layer to activate in-context mitigations |

This structure ensures that:
1. **Developers/operators** know which mitigations require infrastructure-level changes
2. **AI systems** know which defensive behaviors they can apply immediately from reading this guide
3. **End users** know what they can prompt to activate in-context defenses

---

## Attack Classes

> This taxonomy is aligned with [MITRE ATLAS](https://atlas.mitre.org/) (Adversarial Threat Landscape for Artificial-Intelligence Systems) and covers the major categories of attacks targeting AI/ML systems.

### Prompt and Input Attacks

| Class | Name | Primary Risk |
|-------|------|--------------|
| [1](attack-class-1-prompt-injection.md) | Prompt Injection | Instruction override via embedded commands |
| [2](attack-class-2-indirect-prompt-injection.md) | Indirect Prompt Injection | Attacks via external content (web, email, docs) |
| [5](attack-class-5-jailbreaking.md) | Jailbreaking and Instruction Override | Bypassing safety guardrails |
| [12](attack-class-12-evasion-adversarial.md) | Evasion and Adversarial Inputs | Crafted inputs causing misclassification |

### Data and Privacy Attacks

| Class | Name | Primary Risk |
|-------|------|--------------|
| [3](attack-class-3-data-exfiltration.md) | Data Exfiltration via AI | Extracting training data or context |
| [10](attack-class-10-model-inversion.md) | Model Inversion and Membership Inference | Reconstructing training data from model outputs |
| [11](attack-class-11-model-extraction.md) | Model Extraction and Stealing | Recreating models through query access |

### Supply Chain and Training Attacks

| Class | Name | Primary Risk |
|-------|------|--------------|
| [9](attack-class-9-model-supply-chain.md) | Model Supply Chain Compromise | Trojaned models and compromised ML artifacts |
| [13](attack-class-13-training-data-poisoning.md) | Training Data Poisoning | Backdoors and biases embedded during training |
| [6](attack-class-6-retrieval-poisoning.md) | Adversarial Retrieval Poisoning | Planting malicious content in retrieval sources |

### Trust and Integrity Attacks

| Class | Name | Primary Risk |
|-------|------|--------------|
| [4](attack-class-4-fabricated-citations.md) | Misleading or Fabricated Citations | False references appearing legitimate |
| [7](attack-class-7-social-engineering.md) | Social Engineering via AI Persona | Building false trust to exploit users |
| [8](attack-class-8-citation-source-integrity.md) | Citation Source Integrity Attacks | Tampering with cited source content |

### Agentic and Autonomous System Attacks

| Class | Name | Primary Risk |
|-------|------|--------------|
| [14](attack-class-14-agentic-attacks.md) | AI Agent and Agentic System Attacks | Tool abuse, multi-agent escalation, memory poisoning |

---

## How to Use

1. **For AI agents:** Read all attack class descriptions to understand the threat landscape. Use the "How to Detect" sections as patterns to watch for during normal operation, and the "How to Mitigate" sections as guidance when you detect an attack.
2. **For developers:** Use these as requirements for defensive controls.
3. **For security researchers:** Use as a taxonomy for categorizing new attacks.

---

## Contributing

To propose a new attack class, see [contributor-guide.md](../contributor-guide.md#what-to-contribute).
