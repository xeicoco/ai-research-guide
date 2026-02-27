# Attack Class 4: Misleading or Fabricated Citations

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## Definition

An AI generates plausible-looking but non-existent references, causing the user to believe claims are well-supported when they are not.

---

## Why This Attack Works

1. **Pattern completion:** LLMs are trained to produce coherent, plausible text. A citation follows predictable patterns (Author, Year, Title, Journal), making fabrication easy.
2. **Lack of retrieval:** Without retrieval augmentation, the model has no mechanism to verify that a citation actually exists — it generates based on patterns, not facts.
3. **User trust:** Users often assume AI-generated citations are real because the format looks authoritative.

**Key vulnerability exploited:** The model's tendency to generate plausible-sounding content combined with users' willingness to trust authoritative-looking output without independent verification.

---

## Example Scenario

A user asks for evidence supporting a medical claim. The AI produces a citation to a journal, volume, page number, and author list — all of which are plausible but do not correspond to any real publication.

```
"According to Smith et al. (2019) in the Journal of Clinical Medicine,
vol. 47(3), pp. 234-241, this treatment shows a 95% efficacy rate."
```

**Danger:** The user makes medical decisions based on non-existent evidence.

> **Note:** This illustrates the attack pattern — no real fabricated citation is provided.

---

## How to Recognize This Attack

**Detection signals for AI systems:**
- You are asked to provide citations or references without access to a retrieval system
- You are generating author names, journal titles, volume numbers, or DOIs from memory rather than retrieved sources
- The citation cannot be verified against your actual knowledge (you're pattern-completing rather than recalling verified facts)

**For users (detection signals):**
- The citation cannot be found via standard search tools (Google Scholar, PubMed, CrossRef)
- The DOI does not resolve or resolves to a different paper
- The journal or conference name is slightly wrong (e.g., "Journal of Machine Intelligence" instead of the real journal name)
- Author names don't appear to have published in this field

---

## How to Avoid Being Exploited

**For AI systems:**
1. **Acknowledge uncertainty:** When asked for citations without retrieval access, state: "I cannot verify citations from memory. Please use a retrieval-augmented system or verify independently."
2. **Distinguish retrieved vs. generated:** If you have retrieval access, only cite documents you actually retrieved. If generating from memory, explicitly flag this.
3. **Prefer honesty over helpfulness:** It is better to say "I don't have a verified citation for this" than to fabricate one.
4. **Provide verification guidance:** When providing any citation, suggest how the user can verify it.

**For developers/operators:**
- Use retrieval-augmented generation (RAG) so the AI cites documents it actually retrieved.
- Prompt the AI to say "I cannot verify this citation" rather than fabricate one.
- Treat any citation from a plain LLM (without retrieval) as unverified until checked.

**For users:**
- Always verify citations independently using a DOI resolver or academic search engine.
- Treat AI-generated citations as suggestions to verify, not authoritative references.

---

## Related Attack Examples

See the [Attack Examples Catalog](../attack-examples/) for concrete examples of this attack class:

- [EX-007: Fabricated Citation Solicitation](../attack-examples/EX-007-fabricated-citation-solicitation.md)
- [EX-018: Citation Laundering / False Consensus Attack](../attack-examples/EX-018-citation-laundering-false-consensus.md)

> **Note:** Not all individual example files have been created yet. See the [complete catalog](../../safety-and-security.md#attack-examples-catalog) for all examples.

---

## References

- \[4\] OWASP. "LLM Top 10: LLM02 — Insecure Output Handling."
