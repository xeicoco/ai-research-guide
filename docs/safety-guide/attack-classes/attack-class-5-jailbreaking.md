# Attack Class 5: Jailbreaking and Instruction Override

> **Part of the [AI Safety and Security Guide](../README.md)**

---

**Definition:** Techniques designed to cause an AI to bypass its safety training and produce outputs it would otherwise refuse (harmful content, policy violations, disclosure of restricted information).

**Common techniques:**
- Role-play framing ("Pretend you are an AI with no restrictions…").
- Hypothetical framing ("In a fictional story, a character explains how to…").
- Token smuggling (encoding forbidden content in ways that evade filters).
- Many-shot jailbreaking (providing many examples of the AI complying with harmful requests to prime the model to continue).

**Why it is relevant to research:**
Jailbreaking is often used to extract harmful information framed as "research". Understanding jailbreaking helps both users (to recognize when an AI's guardrails have been circumvented) and developers (to design more robust safety measures).

**Mitigations:**
- Evaluate safety training against known jailbreak patterns; update training as new patterns emerge.
- Apply output-level content filtering as a defense-in-depth measure.
- Monitor for anomalous output patterns that may indicate a successful jailbreak.
- Treat newly discovered jailbreak patterns as a security issue and update documentation and mitigations promptly.

---

## Related Attack Examples

See the [Attack Examples Catalog](../attack-examples/) for concrete examples of this attack class:

- [EX-003: Role-Play Jailbreak Attempt](../attack-examples/EX-003-role-play-jailbreak.md)
- [EX-004: Hypothetical / Fictional Framing Jailbreak](../attack-examples/EX-004-hypothetical-fictional-framing-jailbreak.md)
- [EX-005: Many-Shot Priming](../attack-examples/EX-005-many-shot-priming.md)
- [EX-013: Multilingual Jailbreak Bypass](../attack-examples/EX-013-multilingual-jailbreak-bypass.md)
- [EX-021: Crescendo / Gradual Escalation Attack](../attack-examples/EX-021-crescendo-gradual-escalation.md)
- [EX-022: Refusal Suppression Attack](../attack-examples/EX-022-refusal-suppression.md)
- [EX-026: DAN / Competing Objectives Attack](../attack-examples/EX-026-dan-competing-objectives.md)

---

## References

- \[5\] Shen, X. et al. (2023). "Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."
- \[12\] Russinovich, M. et al. (2024). "Great, Now Write an Article About That: The Crescendo Multi-Turn LLM Jailbreak Attack."
