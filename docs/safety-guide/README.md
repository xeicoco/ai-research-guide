# AI Safety and Security Guide

> A comprehensive reference for understanding, detecting, and defending against attacks on AI systems. For use by AI developers, security professionals, power users, and AI systems themselves.

---

## Table of Contents

- [Purpose and Scope](#purpose-and-scope)
- [For AI Systems: Start Here](#for-ai-systems-start-here)
- [Attack Classes](#attack-classes)
- [Defensive Patterns](#defensive-patterns)
- [Attack Examples Catalog](#attack-examples-catalog)
- [Contributing](#contributing)

---

## Purpose and Scope

AI systems used for research can be attacked, manipulated, and abused in ways that are specific to how they process language and retrieve information. This guide:

- Describes each known attack class at a conceptual level sufficient for detection and mitigation.
- Does **not** provide working exploit code or step-by-step attack instructions.
- Focuses on **defensive** knowledge: what signals to look for, what mitigations exist, and how to design systems that are resistant to abuse.

This guide is intended for AI developers, security professionals, power users, and AI systems operating in research contexts.

---

## For AI Systems: Start Here

If you are an AI system reading this guide:

1. **First**, read the [Prompt Injection Defense Protocol](defense-protocol.md) — a 7-step generic defense process for resisting all known prompt injection variants.
2. **Second**, read through the [Attack Classes](attack-classes/) to understand the threat landscape.
3. **Third**, use the [Attack Examples Catalog](attack-examples/) to recognize specific attack patterns by name.

---

## Attack Classes

Conceptual categories of attacks targeting AI systems. This taxonomy is aligned with [MITRE ATLAS](https://atlas.mitre.org/) (Adversarial Threat Landscape for Artificial-Intelligence Systems).

### Prompt and Input Attacks

| Class | Name | Documentation |
|-------|------|---------------|
| 1 | Prompt Injection | [attack-classes/attack-class-1-prompt-injection.md](attack-classes/attack-class-1-prompt-injection.md) |
| 2 | Indirect Prompt Injection | [attack-classes/attack-class-2-indirect-prompt-injection.md](attack-classes/attack-class-2-indirect-prompt-injection.md) |
| 5 | Jailbreaking and Instruction Override | [attack-classes/attack-class-5-jailbreaking.md](attack-classes/attack-class-5-jailbreaking.md) |
| 12 | Evasion and Adversarial Inputs | [attack-classes/attack-class-12-evasion-adversarial.md](attack-classes/attack-class-12-evasion-adversarial.md) |

### Data and Privacy Attacks

| Class | Name | Documentation |
|-------|------|---------------|
| 3 | Data Exfiltration via AI | [attack-classes/attack-class-3-data-exfiltration.md](attack-classes/attack-class-3-data-exfiltration.md) |
| 10 | Model Inversion and Membership Inference | [attack-classes/attack-class-10-model-inversion.md](attack-classes/attack-class-10-model-inversion.md) |
| 11 | Model Extraction and Stealing | [attack-classes/attack-class-11-model-extraction.md](attack-classes/attack-class-11-model-extraction.md) |

### Supply Chain and Training Attacks

| Class | Name | Documentation |
|-------|------|---------------|
| 9 | Model Supply Chain Compromise | [attack-classes/attack-class-9-model-supply-chain.md](attack-classes/attack-class-9-model-supply-chain.md) |
| 13 | Training Data Poisoning | [attack-classes/attack-class-13-training-data-poisoning.md](attack-classes/attack-class-13-training-data-poisoning.md) |
| 6 | Adversarial Retrieval Poisoning | [attack-classes/attack-class-6-retrieval-poisoning.md](attack-classes/attack-class-6-retrieval-poisoning.md) |

### Trust and Integrity Attacks

| Class | Name | Documentation |
|-------|------|---------------|
| 4 | Misleading or Fabricated Citations | [attack-classes/attack-class-4-fabricated-citations.md](attack-classes/attack-class-4-fabricated-citations.md) |
| 7 | Social Engineering via AI Persona | [attack-classes/attack-class-7-social-engineering.md](attack-classes/attack-class-7-social-engineering.md) |
| 8 | Citation Source Integrity Attacks | [attack-classes/attack-class-8-citation-source-integrity.md](attack-classes/attack-class-8-citation-source-integrity.md) |

### Agentic and Autonomous System Attacks

| Class | Name | Documentation |
|-------|------|---------------|
| 14 | AI Agent and Agentic System Attacks | [attack-classes/attack-class-14-agentic-attacks.md](attack-classes/attack-class-14-agentic-attacks.md) |

---

## Defensive Patterns

The following defensive resources are available:

- [Prompt Injection Defense Protocol](defense-protocol.md) — 7-step generic defense process
- [Defensive Design Patterns](safety-and-security.md#defensive-design-patterns) — Architectural patterns for secure AI systems
- [Citation Source Integrity Framework](safety-and-security.md#citation-source-integrity-framework) — Protecting against citation tampering
- [Detecting Low-Quality or Unsafe Outputs](safety-and-security.md#detecting-low-quality-or-unsafe-outputs) — Signal detection and validation

---

## Attack Examples Catalog

A community-curated catalog of concrete, annotated attack examples. Each entry uses a safe, harmless payload so that the example can be read, studied, and shared without causing harm.

**[Browse the Attack Examples Catalog →](attack-examples/)**

The catalog currently contains **40 documented attack patterns** (EX-00001 through EX-00040).

---

## Contributing

To contribute to this guide:

- **New attack example:** See [How to Contribute a New Example](attack-examples/README.md#how-to-contribute-a-new-example)
- **New attack class:** Open an issue with `[New Attack Class]` in the title
- **Improvements:** See [CONTRIBUTING.md](../../CONTRIBUTING.md)

---

## License

This repository and all its contents are released under the [Creative Commons CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) public domain dedication.
