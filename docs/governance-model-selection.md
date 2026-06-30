# Governance Model Selection

> **Authority Class:** Authoritative
> **SDD Authority:** §17.3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 7

---

## 1. Purpose

This document fulfills the §17.3 mandate: "Phase 7 MUST compare and select among documented governance models and justify the choice in context." [Ref: §17.3] It presents three governance model options, defines a comparison framework, and records the selection criteria against which the organization shall evaluate and select the model appropriate to its scale and trust structure. [Ref: §17.3 "Each is appropriate to a different scale and trust structure."]

This document does **not** itself select a model; it provides the framework and evidence base for the selection decision, which **must** be recorded as an ADR per GV-5. [Ref: GV-5]

---

## 2. Normative Requirement

§17.3 imposes the following normative requirements on Phase 7:

- **MUST** compare the three documented governance models. [Ref: §17.3]
- **MUST** justify the selected choice in the organization's context. [Ref: §17.3]
- **MUST** recognize that each model is appropriate to a different scale and trust structure. [Ref: §17.3]

Additionally, the selection **MUST** be consistent with:

- GV-3: changes approved by Standard Authority after Inspection. [Ref: §17.2 GV-3]
- GV-7: roles defined (Standard Authority, Maintainer, Reviewer, Contributor/Project). [Ref: §17.2 GV-7]
- PR-10: controlled evolution; standard changes only through governance. [Ref: PR-10]

---

## 3. Model Options

### 3.1 BDFL/Single-Authority

| Field | Value |
|---|---|
| **Name** | Benevolent Dictator for Life / Single-Authority |
| **Structure** | A single individual holds final decision authority over all changes to the standard. |
| **Evidence base** | Converged practice — characteristic of early-stage standards and founder-led organizations. [Ref: §17.3] |
| **Decision flow** | Proposals → Review → BDFL decides → Accepted/Rejected. |
| **Role mapping** | The BDFL is the Standard Authority (STK-1). Maintainers, Reviewers, and Contributors operate under the BDFL's authority. |

**Characteristics:**

- **Speed:** High; single decision point eliminates coordination latency.
- **Consistency:** High; single vision reduces divergence.
- **Scalability:** Low; bottlenecked by one person's capacity.
- **Bus factor:** Low; concentrated authority creates continuity risk.
- **Trust requirement:** Requires the organization to vest sole authority in one individual.

**Appropriate context:** Small organization; single clear authority; founder-led standard; early-stage adoption where speed of decision outweighs distributed legitimacy. [Ref: §17.3]

### 3.2 Maintainer-Hierarchy

| Field | Value |
|---|---|
| **Name** | Maintainer-Hierarchy |
| **Structure** | Authority is distributed across a hierarchy of maintainers, each responsible for a domain or subsystem, with a top-level maintainer (or small council) resolving cross-cutting changes. |
| **Evidence base** | Linux kernel development process. [Ref: §17.3; Appendix A] |
| **Decision flow** | Proposals → Domain maintainer review → Subsystem maintainer approval → Top-level maintainer approval for cross-cutting changes → Accepted/Rejected. |
| **Role mapping** | Top-level maintainer(s) function as Standard Authority (STK-1). Subsystem maintainers are Maintainers. Reviewers are drawn from the maintainer pool and broader community. Contributors/Projects submit proposals. |

**Characteristics:**

- **Speed:** Medium-high for domain-local changes; lower for cross-cutting changes.
- **Consistency:** Medium; distributed authority can produce localized divergence.
- **Scalability:** High; hierarchy distributes workload across many individuals.
- **Bus factor:** Medium-high; no single point of failure but top-level remains critical.
- **Trust requirement:** Requires trust in the hierarchy's technical judgment and conflict-resolution procedures.

**Appropriate context:** Medium-to-large organization; multiple engineering domains; sufficient engineering depth to staff a multi-level maintainer structure; need for both domain autonomy and standard-wide coherence. [Ref: §17.3]

### 3.3 Committee/Foundation

| Field | Value |
|---|---|
| **Name** | Committee/Foundation |
| **Structure** | A formal committee or foundation board holds decision authority, operating under published bylaws with defined membership, voting procedures, and term limits. |
| **Evidence base** | Apache Software Foundation governance; CNCF governance; IETF RFC process. [Ref: §17.3; Appendix A] |
| **Decision flow** | Proposals → Working group review → Committee vote → Ratification → Accepted/Rejected. |
| **Role mapping** | The committee/board is the Standard Authority (STK-1). Officers or appointed individuals function as Maintainers. Reviewers are committee members and invited experts. Contributors/Projects submit proposals through formal channels. |

**Characteristics:**

- **Speed:** Low; formal process introduces coordination and procedural latency.
- **Consistency:** High; formal process ensures comprehensive review and broad consensus.
- **Scalability:** High; institutional structure is designed for large-scale, multi-stakeholder governance.
- **Bus factor:** High; institutional continuity independent of any individual.
- **Trust requirement:** Requires trust in the institution and its processes rather than in individuals.

**Appropriate context:** Large organization; multiple stakeholder groups; need for institutional legitimacy; regulatory or external certification requirements; long-term durability independent of individual contributors. [Ref: §17.3]

---

## 4. Comparison Framework

The following framework **MUST** be used to evaluate and compare the three models in the organization's specific context. [Ref: §17.3]

| Criterion | Weighting Guidance | BDFL | Maintainer-Hierarchy | Committee/Foundation |
|---|---|---|---|---|
| **Decision speed** | Time from proposal to verdict | High | Medium-High | Low |
| **Scalability** | Ability to handle increasing proposal volume | Low | High | High |
| **Continuity risk** | Susceptibility to individual departure | High | Medium | Low |
| **Domain coverage** | Ability to cover multiple engineering domains | Low | High | High |
| **Process overhead** | Administrative burden of governance | Low | Medium | High |
| **Institutional legitimacy** | Recognizability to external parties | Low | Medium | High |
| **Conformance to GV-3** | Standard Authority approves after Inspection | Yes | Yes (top-level) | Yes (committee) |
| **Conformance to GV-7** | All four roles defined | Yes | Yes | Yes |
| **Evidence quality** | Ability to enforce evidence-based changes | High (single standard) | Medium (distributed) | High (institutional) |

**Selection method:** The organization **MUST** score each model against the criteria above, weight criteria by organizational priority, and select the model with the highest weighted score. The selection **MUST** be recorded as an ADR per GV-5. [Ref: GV-5]

---

## 5. Selection Criteria

The following criteria **MUST** govern the selection decision:

1. **Scale alignment.** The selected model **MUST** be capable of handling the organization's current and projected proposal volume. [Ref: §17.3]
2. **Trust structure alignment.** The selected model **MUST** be compatible with the organization's trust structure (individual-based vs. institution-based). [Ref: §17.3]
3. **Role conformance.** The selected model **MUST** accommodate all four GV-7 roles (Standard Authority, Maintainer, Reviewer, Contributor/Project). [Ref: GV-7]
4. **GV-3 conformance.** The selected model **MUST** preserve the requirement that changes are approved by the Standard Authority after Inspection. [Ref: GV-3]
5. **Evidence basis.** The selection **MUST** be supported by evidence from the approved evidence base (Appendix A) or marked UNSUPPORTED. [Ref: GV-4; PR-1]

SDD does not specify a default or recommended model. [Ref: §17.3]

---

## 6. Completion Criteria

This document is complete when:

1. The §17.3 normative requirement is stated (§2). [Ref: §17.3]
2. All three governance models are documented with structure, evidence base, characteristics, and appropriate context (§3). [Ref: §17.3]
3. A comparison framework with evaluative criteria is provided (§4). [Ref: §17.3]
4. Selection criteria governing the decision are stated (§5). [Ref: §17.3]
5. The selection is recorded as an ADR per GV-5. SDD does not specify who performs this recording. [Ref: GV-5]

---

*END OF DOCUMENT*
