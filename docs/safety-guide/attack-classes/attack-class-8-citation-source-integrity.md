# Attack Class 8: Citation Source Integrity Attacks

> **Part of the [AI Safety and Security Guide](../README.md)**

---

**Definition:** An attacker tampers with or replaces the content at a URL or domain that is cited by an authoritative reference (such as this guide), causing an AI system that fetches or trusts that source to receive false or malicious information — even though the citation itself looks legitimate.

**Example scenario:**
An academic paper cited in this guide originally lived at `https://arxiv.org/abs/XXXX.XXXXX`. Years later, the preprint is updated by the authors to contain a poisoned version, or a cited website's domain expires and is re-registered by an adversary who replaces the content with misleading or malicious material. An AI that retrieves the current content of that URL would ingest the tampered content as if it were the trusted source.

**Why it works:**
AI systems that follow citations as live hyperlinks have no inherent ability to verify that the content at the URL today is the same as when the citation was written. Domain hijacking, URL reassignment, server-side content replacement, and CMS compromise are all realistic supply-chain threats.

**Detection signals:**
- The content at a cited URL contradicts what the citing document says it contains.
- A previously authoritative domain now redirects unexpectedly or serves different content.
- The citation's publication metadata (author names, dates, journal names) no longer matches what the retrieved page presents.

**Mitigations:**
- Prefer persistent identifiers (DOIs, arXiv IDs, ISBN) over bare URLs wherever possible; these are harder to redirect.
- Cross-validate key claims from a citation against at least two additional independent sources before treating the claim as confirmed.
- Treat any retrieved source content that contradicts the citing document's description of it as a potential tampering signal.
- For high-stakes decisions, use archived versions of cited sources (e.g., Wayback Machine snapshots) and note the access date.
- See the [Citation Source Integrity Framework](../citation-source-integrity-framework.md) for a detailed treatment.

---

## Related Attack Examples

See the [Attack Examples Catalog](../attack-examples/) for concrete examples of this attack class:

- [EX-014: Compromised Citation Source Attack](../attack-examples/EX-014-compromised-citation-source.md)
- [EX-018: Citation Laundering / False Consensus Attack](../attack-examples/EX-018-citation-laundering-false-consensus.md)
