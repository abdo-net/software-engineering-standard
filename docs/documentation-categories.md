# Documentation Categories

> **Authority Class:** Authoritative
> **SDD Authority:** §38.2, §38.3, §31.2, §11.1
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the nine documentation categories of the Engineering Documentation Model. [Ref: §38.2] Each documentation unit SHALL be classified as exactly one of these categories. [Ref: §38.2] These categories map to §31 knowledge classes and §11 authority classes, ensuring documentation is categorized, non-mixed, and aligned to the Artifact Authority Model and the Repository Knowledge Architecture. [Ref: §38.1]

## 2. Scope

This document specifies:

1. The nine documentation categories from §38.2: Observed, Verified, Planned, Implemented, Validated, Historical, Deprecated, Generated, Authoritative.
2. The normative documentation rules (DOC-1..DOC-5) from §38.3.
3. The Authority Class mapping for each category (§11.1).
4. The Knowledge Class mapping for each category (§31.2).

## 3. Category Definitions

### 3.1 Observed

**Definition:** Documentation containing raw facts captured during discovery, prior to verification. [Ref: §38.2, §31.2]

**Authority Class:** Non-authoritative (raw observation). [Ref: §11.1]

**Knowledge Class:** Observed Facts [Ref: §31.2]

**Description:** Observed documentation contains raw, pre-verification data captured during the Discovery phase (§25). [Ref: §25] It includes inventory data, structure observations, runtime observations, and other raw capture outputs. Observed documentation MUST NOT be presented as Verified or Validated without passing the Evidence Chain (§28) and Validation (§16). [Ref: §38.3, DOC-4]

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Observed` | §38.2 |
| Authority Class | Non-authoritative | §31.2 |
| Confidence Level | A, B, or E per §26.2 | §31.2 |
| Provenance | Source of observation | §26.3, KN-1 |
| Verification Status | Unverified | §26.3 |

**Rules:**

- Observed documentation MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §26, §28]
- Observed documentation MUST NOT be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16). [Ref: §38.3, DOC-4]

### 3.2 Verified

**Definition:** Documentation containing facts that have passed the Evidence Chain verification. [Ref: §38.2, §31.2]

**Authority Class:** Candidate-authoritative. [Ref: §31.2]

**Knowledge Class:** Verified Facts [Ref: §31.2]

**Description:** Verified documentation contains facts that have passed the Evidence → Verification link of the Evidence Chain (§28). [Ref: §28.2] These facts have been confirmed by evidence and carry a confidence classification (§26), but may not yet have been synthesized into Engineering Knowledge.

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Verified` | §38.2 |
| Authority Class | Candidate-authoritative | §31.2 |
| Confidence Level | A–D per §26.2 (not E) | §31.2, EVC-3 |
| Verification Status | Verified | §26.3 |
| Provenance | Complete chain of custody | §28, ECH-2 |

**Rules:**

- Verified documentation MUST have passed the Verification link per ECH-1. [Ref: §28.3, ECH-1]
- Hypotheses (confidence E) MUST NOT be classified as Verified. [Ref: EVC-3, ECH-5]

### 3.3 Planned

**Definition:** Documentation describing intended design, architecture, or work that is planned but not yet implemented. [Ref: §38.2]

**Authority Class:** Authoritative (for the plan itself). [Ref: §11.1]

**Knowledge Class:** Engineering Knowledge / Design Decisions [Ref: §31.2]

**Description:** Planned documentation contains design documents, ADRs, plans, and other artifacts describing work that is intended but not yet realized. [Ref: §12.2 Planning] Planned documentation is authoritative for the plan itself but MUST NOT be presented as Implemented or Validated. [Ref: §38.3, DOC-4]

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Planned` | §38.2 |
| Authority Class | Authoritative | §11.1 |
| Knowledge Class | Engineering Knowledge | §31.2 |
| Governance Status | Approved per §17 | §35, DEC-1 |
| Linked Decisions | Decision references | §35, DEC-4 |

**Rules:**

- Planned documentation MUST NOT be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16). [Ref: §38.3, DOC-4]
- Plans MUST trace to approved Decisions. [Ref: §35, DEC-4]

### 3.4 Implemented

**Definition:** Documentation describing realized code, configuration, or system elements. [Ref: §38.2]

**Authority Class:** Authoritative (for the implementation record). [Ref: §11.1]

**Knowledge Class:** Engineering Knowledge [Ref: §31.2]

**Description:** Implemented documentation records the actual realization of an approved decision. [Ref: §12.2 Implementation] Every Implementation MUST trace back to exactly one engineering Decision. [Ref: §35.3, DEC-4] Implemented documentation is the record of what was built, not the code itself.

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Implemented` | §38.2 |
| Authority Class | Authoritative | §11.1 |
| Knowledge Class | Engineering Knowledge | §31.2 |
| Decision Reference | Authorizing decision | §35.3, DEC-4 |
| Validation Reference | Validation evidence | §16, VL-4 |

**Rules:**

- Every Implementation MUST trace back to exactly one engineering Decision. [Ref: §35.3, DEC-4]
- INT-1: Every implementation MUST trace to a Decision and documentation. [Ref: §40, INT-1]

### 3.5 Validated

**Definition:** Documentation that has passed objective conformance verification. [Ref: §38.2, §16]

**Authority Class:** Authoritative. [Ref: §11.1]

**Knowledge Class:** Engineering Knowledge [Ref: §31.2]

**Description:** Validated documentation has passed the Validation phase (§16) with objective pass/fail criteria. [Ref: §16.4, VL-1] A conformance verdict MUST cite the evidence on which it rests. [Ref: §16.4, VL-4] Validated documentation represents the highest assurance level for documentation accuracy.

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Validated` | §38.2 |
| Authority Class | Authoritative | §11.1 |
| Knowledge Class | Engineering Knowledge | §31.2 |
| Validation Verdict | Pass / Fail | §16.4, VL-1 |
| Validation Evidence | Reference to evidence | §16.4, VL-4 |
| Validation Method | I / A / D / T per §16.2 | §16.2 |

**Rules:**

- Conformance MUST be expressed as objective pass/fail against stated criteria, never as subjective judgment. [Ref: §16.4, VL-1]
- Validation evidence MUST be recorded and reproducible. [Ref: §16.4, VL-3]
- A conformance verdict MUST cite the evidence on which it rests. [Ref: §16.4, VL-4]

### 3.6 Historical

**Definition:** Documentation that is superseded but retained for traceability. [Ref: §38.2, §31.2]

**Authority Class:** Authoritative-historical (non-governing). [Ref: §31.2]

**Knowledge Class:** Historical Knowledge [Ref: §31.2]

**Description:** Historical documentation is superseded knowledge that has been retained for traceability purposes. [Ref: §31.2] It is non-governing but MUST be retained and marked, not deleted. [Ref: §38.3, DOC-5; §31.3, RKA-3]

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Historical` | §38.2 |
| Authority Class | Authoritative-historical | §31.2 |
| Knowledge Class | Historical Knowledge | §31.2 |
| Superseded By | Reference to replacement | §31.3, RKA-3 |
| Supersede Date | ISO 8601 | §18 |

**Rules:**

- Historical documentation MUST be retained and marked, not deleted. [Ref: §38.3, DOC-5]
- RKA-3: Superseded knowledge MUST be retained as Historical; deprecated knowledge MUST be marked, not deleted. [Ref: §31.3, RKA-3]
- Supersedes relationships MUST preserve the superseded object as Historical. [Ref: §44.3, REL-4]

### 3.7 Deprecated

**Definition:** Documentation marked obsolete, retained for traceability. [Ref: §38.2, §31.2]

**Authority Class:** Non-governing. [Ref: §31.2]

**Knowledge Class:** Deprecated Knowledge [Ref: §31.2]

**Description:** Deprecated documentation is marked obsolete but retained for traceability. [Ref: §31.2] It is non-governing and MAY indicate planned removal per the deprecation policy (VS-6). [Ref: §18, VS-6]

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Deprecated` | §38.2 |
| Authority Class | Non-governing | §31.2 |
| Knowledge Class | Deprecated Knowledge | §31.2 |
| Deprecation Date | ISO 8601 | §18, VS-6 |
| Replacement Reference | Reference to replacement (if any) | §18, VS-4 |

**Rules:**

- Deprecated documentation MUST be retained and marked, not deleted. [Ref: §38.3, DOC-5]
- RKA-3: Deprecated knowledge MUST be marked, not deleted. [Ref: §31.3, RKA-3]
- The standard SHOULD define a deprecation period for rules being removed. [Ref: §18, VS-6]

### 3.8 Generated

**Definition:** Documentation mechanically produced from authoritative sources or from the system under engineering. [Ref: §38.2, §11.1]

**Authority Class:** Generated. [Ref: §11.1]

**Knowledge Class:** Generated Knowledge [Ref: §31.2]

**Description:** Generated documentation is mechanically produced and MUST NOT be hand-edited. [Ref: §11.1, §38.3, DOC-3] It MUST be reproducible from its authoritative sources. [Ref: RA-4] Examples include dependency graphs, API reference from contracts, and traceability indexes. [Ref: §11.3]

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Generated` | §38.2 |
| Authority Class | Generated | §11.1 |
| Knowledge Class | Generated Knowledge | §31.2 |
| Generation Source | Authoritative source pointer(s) | §11.2, RA-4 |
| Generation Procedure | Tool/script reference | RA-4 |
| Generated At | ISO 8601 timestamp | §11.2 |

**Rules:**

- Generated documentation MUST NOT be hand-edited and MUST be reproducible. [Ref: §38.3, DOC-3; RA-4]
- RKA-4: Generated and Derived knowledge MUST NOT be hand-edited; they MUST be reproducible from authoritative sources. [Ref: §31.3, RKA-4]

### 3.9 Authoritative

**Definition:** Documentation that is the single source of truth for some fact or decision. [Ref: §38.2, §11.1]

**Authority Class:** Authoritative. [Ref: §11.1]

**Knowledge Class:** Authoritative Knowledge [Ref: §31.2]

**Description:** Authoritative documentation is the single source of truth for some fact or decision. [Ref: §11.1] It is hand-authored and MAY be edited by humans through review and governance. [Ref: §11.1] The SDD itself is an authoritative artifact. [Ref: §11.1] Authoritative documentation introduces normative rules and is the governing reference for all derived and generated artifacts.

**Mandatory Metadata:**

| Field | Value | Source |
|---|---|---|
| Category | `Authoritative` | §38.2 |
| Authority Class | Authoritative | §11.1 |
| Knowledge Class | Authoritative Knowledge | §31.2 |
| Governance Status | Approved per §17 | §17, GV-3 |
| Review Record | Inspection record per RV-2 | §15, RV-2 |

**Rules:**

- Authoritative documentation MAY be edited by humans through review and governance. [Ref: §11.1]
- Changes to authoritative documentation MUST pass through governance (§17) and versioning (§18). [Ref: §17, §18]
- RA-3: No fact SHALL be authoritative in two places. Cross-references MUST point to the single authoritative artifact. [Ref: §10.3, RA-3]

## 4. Normative Rules (DOC-1..DOC-5)

| ID | Rule | Evidence |
|---|---|---|
| **DOC-1** | Documentation MUST NOT mix the §38.2 categories within one authoritative unit. [Ref: §38.3] | PR-6; ISO 26515 |
| **DOC-2** | Each documentation unit MUST declare its category (§38.2) and its authority class (§11.2). [Ref: §38.3] | §11.2 |
| **DOC-3** | Generated documentation MUST NOT be hand-edited and MUST be reproducible. [Ref: §38.3] | RA-4; PR-6 |
| **DOC-4** | Observed/Planned documentation MUST NOT be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16). [Ref: §38.3] | §28; §16 |
| **DOC-5** | Deprecated/Historical documentation MUST be retained and marked, not deleted. [Ref: §38.3] | RKA-3; RFC 8594 |

## 5. Authority Class Mapping

The following table maps each documentation category to its Artifact Authority Class per §11.1:

| Category | Authority Class | Editing Rule | Source |
|---|---|---|---|
| **Observed** | Non-authoritative | May be edited during discovery | §31.2, §38.2 |
| **Verified** | Candidate-authoritative | May be edited with evidence | §31.2, §38.2 |
| **Planned** | Authoritative | Edited through governance | §11.1, §38.2 |
| **Implemented** | Authoritative | Edited through governance | §11.1, §38.2 |
| **Validated** | Authoritative | Edited through governance | §11.1, §38.2 |
| **Historical** | Authoritative-historical | Retained, not edited | §31.2, §38.2 |
| **Deprecated** | Non-governing | Retained, marked | §31.2, §38.2 |
| **Generated** | Generated | MUST NOT be hand-edited | §11.1, §38.2 |
| **Authoritative** | Authoritative | Edited through governance | §11.1, §38.2 |

## 6. Knowledge Class Mapping

The following table maps each documentation category to its Repository Knowledge Class per §31.2:

| Category | Knowledge Class | Confidence | Source |
|---|---|---|---|
| **Observed** | Observed Facts | A/B/E | §31.2, §38.2 |
| **Verified** | Verified Facts | A–D | §31.2, §38.2 |
| **Planned** | Engineering Knowledge | — | §31.2, §38.2 |
| **Implemented** | Engineering Knowledge | — | §31.2, §38.2 |
| **Validated** | Engineering Knowledge | — | §31.2, §38.2 |
| **Historical** | Historical Knowledge | — | §31.2, §38.2 |
| **Deprecated** | Deprecated Knowledge | — | §31.2, §38.2 |
| **Generated** | Generated Knowledge | — | §31.2, §38.2 |
| **Authoritative** | Authoritative Knowledge | — | §31.2, §38.2 |

### Category Progression

Documentation categories SHALL progress through the following path, consistent with the Evidence Chain (§28) and the Information Model (§47):

```
Observed → Verified → Planned → Implemented → Validated
```

- Historical and Deprecated are terminal retention states for superseded knowledge. [Ref: §31.3, RKA-3]
- Generated is a production mechanism, not a lifecycle stage. [Ref: §11.1]
- Authoritative is a quality attribute that applies to Planned, Implemented, and Validated categories. [Ref: §11.1]

## 7. Completion Criteria

This document is complete when:

1. All nine documentation categories from §38.2 are defined with their metadata requirements. [Ref: §38.2]
2. All five normative documentation rules (DOC-1..DOC-5) are stated. [Ref: §38.3]
3. Each category is mapped to its §11.1 Authority Class. [Ref: §11.1, §38.2]
4. Each category is mapped to its §31.2 Knowledge Class. [Ref: §31.2, §38.2]
5. The category progression path is defined consistent with the Evidence Chain (§28). [Ref: §28]
6. The distinction between authoritative and non-authoritative documentation is preserved per DOC-1. [Ref: §38.3, DOC-1]
7. The schema does not introduce requirements, fields, or terminology not present in the SDD. [Ref: §11.4]
