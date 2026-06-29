# Artifact Classification

> **Authority Class:** Authoritative
> **SDD Authority:** §10, §11, §18, §19
> **Status:** Accepted
> **Version:** 0.4.0
> **Phase:** Phase 2

---

## 1. Purpose

This document defines the official artifact classification system for the Software Engineering Standard (SES). Every artifact within the SES repository SHALL be classified according to the model defined herein. [Ref: §11.1]

The classification system is the structural core that prevents documentation drift by establishing, for every artifact: its authority source, its edit policy, its generation policy, and its storage location. [Ref: §11.1]

---

## 2. Normative References

- SDD §10 — Repository Architecture [Ref: §10]
- SDD §11 — Artifact Architecture [Ref: §11]
- SDD §18 — Versioning Strategy [Ref: §18]
- SDD §19 — Extension Policy [Ref: §19]
- SDD §46 — Canonical Engineering Vocabulary [Ref: §46]

---

## 3. Primary Authority Classes

Every artifact the SES recognizes SHALL be classified into exactly one of three primary authority classes. [Ref: §11.1, FR-3]

### 3.1 Authoritative

| Attribute | Specification |
|---|---|
| **Definition** | The single source of truth for some fact or decision. Hand-authored. [Ref: §11.1] |
| **Authority source** | The artifact itself is the authority. No other artifact may override it. [Ref: RA-3, RA-5] |
| **Edit policy** | MAY be edited by humans through review + governance per §17. Changes MUST be versioned per §18. Authoritative artifacts MUST NOT be silently edited; they are superseded, never modified in-place. [Ref: §11.1, §17 GV-5, §18 VS-2, KN-2] |
| **Generation policy** | Hand-authored. Not generated from other artifacts. [Ref: §11.1] |
| **Regenerability** | N/A — Authoritative artifacts are the root of the derivation chain. [Ref: RA-3, RA-4] |
| **Storage location** | `NORMATIVE STANDARD` region of the repository (§10.3). [Ref: §10.3, §10.4] |

**Examples (§11.1):** The SDD; Architecture Decision Records (ADRs); Contract Specifications; Invariant Registers.

**Normative rules:**
- The `NORMATIVE STANDARD` region is the only region that may contain `MUST/SHALL` rules. [Ref: §10.4]
- In any conflict between regions, the Normative Standard governs. [Ref: RA-5]
- Every authoritative artifact SHALL carry, at minimum: a unique identifier, an authority class (§11.1), an owner, a version, a status, and — for derived/generated artifacts — a pointer to the authoritative source(s) from which it is produced. [Ref: §11.2]

---

### 3.2 Derived

| Attribute | Specification |
|---|---|
| **Definition** | Produced by transforming one or more authoritative artifacts; carries no independent truth. [Ref: §11.1] |
| **Authority source** | The authoritative artifact(s) from which it is derived. The derived artifact introduces no independent authority. [Ref: RA-3, §10.4] |
| **Edit policy** | MUST NOT be hand-edited. MUST be regenerated from source. [Ref: §11.1, FR-3] |
| **Generation policy** | Produced by transforming one or more authoritative artifacts through a documented, tool-agnostic procedure. [Ref: RA-4] |
| **Regenerability** | Any derived artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: RA-4] |
| **Storage location** | `DERIVED OPERATIONAL DOCS` region of the repository (§10.3). [Ref: §10.3] |

**Examples (§11.1):** SOP derived from lifecycle; Checklists derived from stages.

**Normative rules:**
- Operational documents, templates, and examples MUST derive their authority by citing the standard and MUST NOT introduce new normative rules. [Ref: §10.4]
- A derived artifact that cannot be regenerated has silently become a second source of truth and is non-conformant. [Ref: RA-4, PR-6]

---

### 3.3 Generated

| Attribute | Specification |
|---|---|
| **Definition** | Mechanically produced from authoritative sources or from the system under engineering. [Ref: §11.1] |
| **Authority source** | The authoritative source(s) or the system under engineering from which it was mechanically produced. [Ref: RA-4, §11.1] |
| **Edit policy** | MUST NOT be hand-edited; MUST be reproducible. [Ref: §11.1, FR-3] |
| **Generation policy** | Mechanically produced from authoritative sources or from the system under engineering by a deterministic procedure. [Ref: RA-4, §11.1] |
| **Regenerability** | Any generated artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: RA-4] |
| **Storage location** | Produced artifacts; storage location determined by generation procedure. Stored in repository as version-controlled artifacts. [Ref: §10, §11] |

**Examples (§11.1):** Dependency graphs; API reference from contracts; Traceability indexes.

**Normative rules:**
- Generated artifacts MUST NOT be hand-edited; they MUST be reproducible from authoritative sources. [Ref: RKA-4]
- The traceability graph SHOULD be a generated artifact, not hand-maintained, to prevent drift. [Ref: TGR-4]
- Appendix C (Requirements Traceability Index) is a generated artifact and MUST be generated, not hand-maintained. [Ref: §11.2 note, §11.3]

---

## 4. Supplementary Classes

The following supplementary classes refine the storage-location categories defined in §10.3. They describe the *role* of the artifact within the repository architecture. Every supplementary class artifact SHALL also carry one of the three primary authority classes defined in §3 above. [Ref: §10.3, §10.4]

### 4.1 Reference

| Attribute | Specification |
|---|---|
| **Definition** | Supporting material — the cited evidence base. Material referenced by authoritative artifacts but not itself normative. [Ref: §10.3] |
| **Primary authority class** | Reference material is not itself authoritative for the standard; it is supporting. Individual items may be authoritative in their external domain (e.g., ISO standards). [Ref: §10.3] |
| **Edit policy** | Reference material SHALL NOT be modified. It may be added to under governance. [Ref: §10.4] |
| **Generation policy** | Collected, not generated. Added as external sources are cited. [Ref: §10.3] |
| **Storage location** | `REFERENCE MATERIAL` region of the repository (§10.3). [Ref: §10.3] |

**Normative rules:**
- Reference material SHALL NOT introduce new normative rules. [Ref: §10.4]
- The evidence base in Appendix A is the approved citation base for the standard. [Ref: Appendix A]

---

### 4.2 Template

| Attribute | Specification |
|---|---|
| **Definition** | A derived artifact that serves as a pattern for instantiating artifacts. Templates provide the structure into which project-specific content is placed. [Ref: §10.3 TEMPLATES] |
| **Primary authority class** | **Derived** — Templates are derived from the standard and SHALL cite the standard rules they instantiate. [Ref: §10.3, §10.4] |
| **Edit policy** | Templates SHALL NOT be edited during instantiation; project-specific content fills the template fields. Changes to the template itself require governance. [Ref: §10.4] |
| **Generation policy** | Derived from authoritative standard specifications (§11, §13, §16) in Phase 8. [Ref: §24] |
| **Storage location** | `TEMPLATES` region of the repository (§10.3). [Ref: §10.3] |

**Planned templates (§24):** ADR template, Contract template, Design document template, Stage template, Checklist template.

**Normative rules:**
- Templates MUST derive their authority by citing the standard and MUST NOT introduce new normative rules. [Ref: §10.4]
- Templates are a Phase-8 deliverable. [Ref: §24]

---

### 4.3 Example

| Attribute | Specification |
|---|---|
| **Definition** | Illustrative material showing how the standard is applied in practice. Examples are non-normative. [Ref: §10.3 EXAMPLES, §10.4] |
| **Primary authority class** | **Reference/Non-normative** — Examples carry no authority and SHALL NOT be cited as rules. [Ref: §10.4] |
| **Edit policy** | Examples MAY be added, removed, or updated under governance. They SHALL NOT be treated as prescriptive. [Ref: §10.4] |
| **Generation policy** | Hand-authored as worked illustrations of standard application. [Ref: §24] |
| **Storage location** | `EXAMPLES` region of the repository (§10.3). [Ref: §10.3] |

**Planned examples (§24):** Worked examples across domains (backend, frontend, infra, reverse engineering, legacy modernization).

**Normative rules:**
- The `NORMATIVE STANDARD` region is the only region that may contain `MUST/SHALL` rules. Operational documents, templates, and examples MUST derive their authority by citing the standard and MUST NOT introduce new normative rules. [Ref: §10.4]
- Examples are a Phase-9 deliverable. [Ref: §24]

---

## 5. Classification Rules

### 5.1 Mandatory Classification

- Every artifact in the SES repository SHALL be classified with exactly one primary authority class from §3. [Ref: §11.1, FR-3]
- Every artifact SHALL additionally declare its supplementary class (if applicable) from §4. [Ref: §10.3, §11.2]

### 5.2 Authority Precedence

- The `NORMATIVE STANDARD` region is authoritative over all other regions. [Ref: RA-5]
- In any conflict, the standard governs. [Ref: RA-5]
- Appendix B (Glossary) is a derived convenience view of the authoritative Canonical Engineering Vocabulary (§46). On conflict, §46 governs. [Ref: VOC-3, CON-2]

### 5.3 Edit Restrictions

- Derived and Generated artifacts MUST NOT be hand-edited. [Ref: §11.1, FR-3]
- Authoritative artifacts MAY be edited only through review + governance. [Ref: §11.1, §17]
- Authoritative decisions (ADRs) are immutable once accepted; they are superseded, never edited. [Ref: §11.3, KN-2]

### 5.4 Metadata Requirements

Every artifact SHALL carry, at minimum, the following metadata: [Ref: §11.2]

| Field | Requirement |
|---|---|
| **Unique identifier** | Object ID per §43.2 |
| **Authority class** | One of: Authoritative / Derived / Generated (§11.1) |
| **Owner** | Single accountable owner per §11.2, §43.2 |
| **Version** | Semantic version per §18 |
| **Status** | Draft / Accepted / Superseded / Deprecated per §11.2 |
| **Source pointer** | For Derived/Generated: pointer to authoritative source(s) (§11.2) |

### 5.5 Regenerability Requirement

Any derived or generated artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: RA-4] A derived or generated artifact that cannot be regenerated has silently become a second source of truth. [Ref: RA-4, PR-6]

---

## 6. Special Artifact Types

The following artifact types are recognized as constitutionally important and SHALL be specified in full in Phase 4. They are named here only to fix their authority class. [Ref: §11.3]

| Artifact Type | Primary Authority Class | Storage Location | Key Properties |
|---|---|---|---|
| **Architecture Decision Record (ADR)** | Authoritative | NORMATIVE STANDARD | Immutable once accepted; superseded, never edited. [Ref: §11.3, KN-2] |
| **Contract Specification** | Authoritative | NORMATIVE STANDARD | The agreed interface + semantics across a boundary. [Ref: §11.3] |
| **Invariant Register** | Authoritative | NORMATIVE STANDARD | Constraints that MUST remain true. [Ref: §11.3] |
| **Provenance Record** | Authoritative | NORMATIVE STANDARD | Links any recorded fact to its source evidence. [Ref: §11.3, PR-5] |
| **Traceability Index** | Generated | Generated artifact | Links principles → requirements → verification. [Ref: §11.3, §48] |

---

## 7. Relationship to Repository Architecture

The classification system maps to the repository architecture defined in §10.3 as follows: [Ref: §10.3]

```
Repository (permanent engineering memory)
│
├── NORMATIVE STANDARD            → Authoritative class (§3.1)
│
├── DERIVED OPERATIONAL DOCS      → Derived class (§3.2)
│
├── REFERENCE MATERIAL            → Reference supplementary class (§4.1)
│
├── TEMPLATES                     → Template supplementary class (§4.2) → Derived class
│
└── EXAMPLES                      → Example supplementary class (§4.3) → Non-normative
```

[Ref: §10.3 architectural view]

---

*End of Artifact Classification. This document is an authoritative artifact per §11.1.*
