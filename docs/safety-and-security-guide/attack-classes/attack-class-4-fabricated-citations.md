# Attack Class 4: Misleading or Fabricated Citations

> **Part of the [AI Safety and Security Guide](../README.md)**

---

## MITRE ATT&CK / ATLAS Mapping

| Framework | Technique ID | Technique Name | Sub-Technique ID | Sub-Technique Name |
|-----------|-------------|----------------|------------------|--------------------|
| MITRE ATLAS | — | — | — | — |
| MITRE ATT&CK | — | — | — | — |


## Definition

An AI generates plausible-looking but non-existent references, causing the user to believe claims are well-supported when they are not.

---

## Why This Attack Works

1. **Pattern completion:** LLMs are trained to produce coherent, plausible text. A citation follows predictable patterns (Author, Year, Title, Journal), making fabrication easy.
2. **Lack of retrieval:** Without retrieval augmentation, the model has no mechanism to verify that a citation actually exists — it generates based on patterns, not facts.
3. **User trust:** Users often assume AI-generated citations are real because the format looks authoritative.

**Key vulnerability exploited:** The model's tendency to generate plausible-sounding content combined with users' willingness to trust authoritative-looking output without independent verification.

---

## Target and Impact

| Aspect | Details |
|--------|---------|
| **Primary Target** | User trust in AI-generated research content and the integrity of knowledge work |
| **Potential Harm** | Misinformation propagation, reliance on false evidence, academic fraud, decision-making based on fabricated data |
| **Affected Parties** | End users (deceived by false references), researchers (academic integrity undermined), general public (misinformation spread), organizations (reputational risk if false claims published) |

---

## Attack Vector

| Aspect | Details |
|--------|---------|
| **Attack Origin** | AI model itself (hallucination during generation), or user prompts specifically requesting citations |
| **Entry Point** | Research queries, citation requests, literature review tasks, summarization requests |
| **Delivery Method** | Plausible-looking but nonexistent author names, journal titles, volume numbers, DOIs, and URLs |

---

## AI E2E Attack Surface

> Maps which layers of the AI end-to-end pipeline this attack **targets** (🎯 Delivered), **exploits** (⚡ Exploited), or where its **harm manifests** (💥 Impact). Use `—` for layers not involved.

| AI E2E Layer | Stage | Notes |
|---|---|---|
| User Interface Layer | 🎯 Delivered | User requests citations, references, or factual claims, triggering the AI to generate sourced content |
| Input Processing Layer | — | — |
| Routing & Orchestration Layer | — | — |
| Memory Retrieval Layer | — | — |
| Knowledge Retrieval Layer (RAG) | ⚡ Exploited | Absence of verified knowledge sources (or weak retrieval) forces the model to fill gaps with fabricated plausible-sounding citations |
| Agent & Tool Execution Layer | — | — |
| Inference & Model Layer | ⚡ Exploited | Model generates convincing but false citations, author names, publication details, or URLs based on statistical patterns rather than verified facts |
| Output Processing Layer | 💥 Impact | Fabricated citations are included in the response without a factual-verification step |
| Delivery Layer | 💥 Impact | False information is delivered to the user as if it were authoritative and real |
| User Response Layer | 💥 Impact | User trusts, cites, or acts upon fabricated references, spreading misinformation |
| Feedback & Learning Loop | — | — |

**Stage key:** 🎯 Delivered — attack enters the pipeline here | ⚡ Exploited — vulnerability exercised here | 💥 Impact — harm manifests here

---
## How to Detect This Attack

### 🧠 Real-Time AI-Learnable Detection
*Detection signals the AI entity can apply in real-time, without infrastructure changes.*

**Detection signals for AI systems:**
- You are asked to provide citations or references without access to a retrieval system
- You are generating author names, journal titles, volume numbers, or DOIs from memory rather than retrieved sources
- The citation cannot be verified against your actual knowledge (you're pattern-completing rather than recalling verified facts)

**For users (detection signals):**
- The citation cannot be found via standard search tools (Google Scholar, PubMed, CrossRef)
- The DOI does not resolve or resolves to a different paper
- The journal or conference name is slightly wrong (e.g., "Journal of Machine Intelligence" instead of the real journal name)
- Author names don't appear to have published in this field

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to prime the AI's in-context detection for this attack:*

> "For this session, flag any citation, reference, source URL, or factual claim you are not confident actually exists in your verified training knowledge. Use a qualifier like 'I cannot confirm this source exists' rather than presenting uncertain citations as verified. Never invent author names, publication years, journal titles, or URLs."

---
## How to Mitigate This Attack

### 🛡️ Infrastructure-Side Mitigations
*Require implementation by developers/operators on the AI infrastructure, model, or service level.*

- Use retrieval-augmented generation (RAG) so the AI cites documents it actually retrieved rather than generating from pattern completion.
- Prompt the AI in the system prompt to say "I cannot verify this citation" rather than fabricate one when retrieval is unavailable.
- Implement citation verification pipelines that validate references against academic databases (CrossRef, DOI, PubMed) before presenting to users.
- Display clear UI indicators distinguishing "retrieved and verified" vs. "generated" content.
- Treat any citation from a plain LLM (without retrieval) as unverified and label it accordingly in the output.

### 🧠 Real-Time AI-Learnable Mitigations
*Can be learned and applied by the AI entity itself in real-time, without infrastructure changes.*

1. **Acknowledge uncertainty:** When asked for citations without retrieval access, state: "I cannot verify citations from memory. Please use a retrieval-augmented system or verify independently."
2. **Distinguish retrieved vs. generated:** If you have retrieval access, only cite documents you actually retrieved. If generating from memory, explicitly flag this: "Note: I'm generating this from patterns in my training, not from a retrieved source."
3. **Prefer honesty over helpfulness:** It is better to say "I don't have a verified citation for this" than to fabricate one.
4. **Provide verification guidance:** When providing any citation, suggest how the user can verify it (e.g., "You can verify this via Google Scholar or the DOI resolver").
5. **Recognize fabrication pressure:** If pressed to provide a citation when you're uncertain, maintain your position: "I'd rather not provide an unverified citation than risk misleading you."

**For users:**
- Always verify citations independently using a DOI resolver or academic search engine.
- Treat AI-generated citations as suggestions to verify, not authoritative references.

### 💬 User Endpoint Teaching Prompts
*Prompts a user can send at the User Interface Layer to activate in-context mitigations for this attack:*

> "For this session, apply citation integrity rules: only present a source as verified if you have high confidence it exists in your training knowledge. Preface uncertain citations with a confidence qualifier. Do not fabricate author names, publication years, journal names, DOIs, or URLs to fill a citation gap — say explicitly that you cannot provide a verified source instead."

---
## Related Attack Examples

See the [Attack Examples Catalog](../attack-examples/) for concrete examples of this attack class:

- [EX-00007: Fabricated Citation Solicitation](../attack-examples/EX-00007-fabricated-citation-solicitation.md)
- [EX-00018: Citation Laundering / False Consensus Attack](../attack-examples/EX-00018-citation-laundering.md)


---

## Example Scenario

A user asks for evidence supporting a medical claim. The AI produces a citation to a journal, volume, page number, and author list — all of which are plausible but do not correspond to any real publication.

```
"According to Smith et al. (2019) in the Journal of Clinical Medicine,
vol. 47(3), pp. 234-241, this treatment shows a 95% efficacy rate."
```

**Danger:** The user makes medical decisions based on non-existent evidence.

> **Note:** This illustrates the attack pattern — no real fabricated citation is provided.
## References

- \[1\] OWASP. "LLM Top 10: LLM02 — Insecure Output Handling."

---

