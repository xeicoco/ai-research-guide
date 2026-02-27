# Attack Class 4: Misleading or Fabricated Citations

> **Part of the [AI Safety and Security Guide](../README.md)**

---

**Definition:** An AI generates plausible-looking but non-existent references, causing the user to believe claims are well-supported when they are not.

**Example scenario:**
A user asks for evidence supporting a medical claim. The AI produces a citation to a journal, volume, page number, and author list — all of which are plausible but do not correspond to any real publication.

**Why it is dangerous:**
Users who trust AI-generated citations without verification may make decisions (medical, legal, financial, academic) based on non-existent evidence. They may also propagate the fabricated citation.

**Detection signals:**
- The citation cannot be found via standard search tools (Google Scholar, PubMed, CrossRef).
- The DOI does not resolve or resolves to a different paper.
- The journal or conference name is slightly wrong (e.g., "Journal of Machine Intelligence" instead of the real journal name).

**Mitigations:**
- Always verify citations independently using a DOI resolver or academic search engine.
- Prompt the AI to say "I cannot verify this citation" rather than fabricate one.
- Use retrieval-augmented generation (RAG) so the AI cites documents it actually retrieved.
- Treat any citation from a plain LLM (without retrieval) as unverified until checked.

---

## Related Attack Examples

See the [Attack Examples Catalog](../attack-examples/) for concrete examples of this attack class:

- [EX-007: Fabricated Citation Solicitation](../attack-examples/EX-007-fabricated-citation-solicitation.md)
- [EX-018: Citation Laundering / False Consensus Attack](../attack-examples/EX-018-citation-laundering-false-consensus.md)

---

## References

- \[4\] OWASP. "LLM Top 10: LLM02 — Insecure Output Handling."
