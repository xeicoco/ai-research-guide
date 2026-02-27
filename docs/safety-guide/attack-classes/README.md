# Attack Classes Index

> **Part of the [AI Safety and Security Guide](../README.md)**

This directory contains detailed documentation for each conceptual attack class targeting AI systems.

---

## Attack Classes

| Class | Name | Primary Risk |
|-------|------|--------------|
| [1](attack-class-1-prompt-injection.md) | Prompt Injection | Instruction override via embedded commands |
| [2](attack-class-2-indirect-prompt-injection.md) | Indirect Prompt Injection | Attacks via external content (web, email, docs) |
| [3](attack-class-3-data-exfiltration.md) | Data Exfiltration via AI | Extracting training data or context |
| [4](attack-class-4-fabricated-citations.md) | Misleading or Fabricated Citations | False references appearing legitimate |
| [5](attack-class-5-jailbreaking.md) | Jailbreaking and Instruction Override | Bypassing safety guardrails |
| [6](attack-class-6-retrieval-poisoning.md) | Adversarial Retrieval Poisoning | Planting malicious content in retrieval sources |
| [7](attack-class-7-social-engineering.md) | Social Engineering via AI Persona | Building false trust to exploit users |
| [8](attack-class-8-citation-source-integrity.md) | Citation Source Integrity Attacks | Tampering with cited source content |

---

## How to Use

1. **For AI agents:** Read all attack class descriptions to understand the threat landscape before processing external content.
2. **For developers:** Use these as requirements for defensive controls.
3. **For security researchers:** Use as a taxonomy for categorizing new attacks.

---

## Contributing

To propose a new attack class, see [CONTRIBUTING.md](../../../CONTRIBUTING.md#contributing-to-security).
