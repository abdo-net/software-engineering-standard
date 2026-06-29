# Artifact Registry

> **Authority Class:** Authoritative
> **SDD Authority:** §10, §11, §24
> **Status:** Accepted
> **Version:** 0.4.0
> **Phase:** Phase 2

---

## 1. Purpose

This document is the canonical registry of ALL artifacts within the Software Engineering Standard (SES) repository — both those that currently exist and those planned per §24 Future Work. [Ref: §11.4, §24]

Every artifact listed herein SHALL carry: a unique name, an artifact class, an authoritative source, an owner, a generation mode (generated or manual), a lifecycle state, and the phase in which it was introduced. [Ref: §11.2, §43.2]

---

## 2. Normative References

- SDD §10 — Repository Architecture [Ref: §10]
- SDD §11 — Artifact Architecture [Ref: §11]
- SDD §17 — Governance Model [Ref: §17]
- SDD §18 — Versioning Strategy [Ref: §18]
- SDD §24 — Future Work [Ref: §24]
- SDD §42 — Engineering Meta-Model [Ref: §42]
- SDD §43 — Engineering Object Model [Ref: §43]

---

## 3. Artifact Registry Table

### 3.1 Existing Artifacts (Phase 2)

The following artifacts exist in the repository as of Phase 2. [Ref: §24 Phase 2 — "Concrete repository directory/file structure"]

| Artifact Name | Artifact Class | Authoritative Source | Owner | Generated/Manual | Lifecycle | Phase Introduced |
|---|---|---|---|---|---|---|
| **SDD.md** | Authoritative | The standard itself; §1–§50 | Standard Authority | Manual | Accepted | Phase 2 |
| **repository-constitution.md** | Authoritative | §7 (Principles), §17 (Governance), §19 (Extension) | Standard Authority | Manual | Accepted | Phase 2 |
| **repository-rules.md** | Authoritative | §8 (FR), §9 (NFR), §23 (Constraints), §40 (Integrity Rules) | Standard Authority | Manual | Accepted | Phase 2 |
| **artifact-classification.md** | Authoritative | §11.1 (Artifact Authority Model) | Standard Authority | Manual | Accepted | Phase 2 |
| **artifact-registry.md** | Authoritative | §11 (Artifact Architecture), §24 (Future Work) | Standard Authority | Manual | Accepted | Phase 2 |
| **dependency-graph.md** | Generated | §45 (Engineering Dependency Graph) | SES Maintainers | Generated | Accepted | Phase 2 |
| **traceability-graph.md** | Generated | §48 (Engineering Traceability Graph), §44 (Relationship Model) | SES Maintainers | Generated | Accepted | Phase 2 |
| **VERSION** | Authoritative | §18 (Versioning Strategy) | Standard Authority | Manual | Accepted | Phase 2 |
| **CHANGELOG.md** | Authoritative | §18 VS-2 (changelog requirement) | Standard Authority | Manual | Accepted | Phase 2 |
| **README.md** | Reference | §1 (Vision), §10 (Repository Architecture) | SES Maintainers | Manual | Accepted | Phase 2 |
| **LICENSE** | Reference | External legal reference; repository requirement | Standard Authority | Manual | Accepted | Phase 2 |
| **.gitignore** | Reference | Git tooling requirement | SES Maintainers | Manual | Accepted | Phase 2 |

### 3.2 Special Artifact Types (§11.3)

The following artifact types are recognized as constitutionally important and SHALL be specified in full in Phase 4. [Ref: §11.3, §24 Phase 4 — "Full artifact catalog + schemas"]

| Artifact Name | Artifact Class | Authoritative Source | Owner | Generated/Manual | Lifecycle | Phase Introduced |
|---|---|---|---|---|---|---|
| **Architecture Decision Record (ADR)** | Authoritative | §11.3, §35 (Decision Model), KN-2 | Decision Author + Standard Authority | Manual | Accepted/Superseded | Phase 4 (template: Phase 8) |
| **Contract Specification** | Authoritative | §11.3, §14.2 (Contracts) | Standard Authority | Manual | Accepted | Phase 4 |
| **Invariant Register** | Authoritative | §11.3, §14.2 (Invariants) | Standard Authority | Manual | Accepted | Phase 4 |
| **Provenance Record** | Authoritative | §11.3, PR-5, §28 (Evidence Chain) | Evidence Producer + Standard Authority | Manual | Accepted | Phase 4 |
| **Traceability Index** | Generated | §11.3, §48 (Traceability Graph), TGR-4 | SES Maintainers | Generated | Accepted | Phase 2 (view); Phase 4 (full) |

### 3.3 Planned Artifacts (§24 Future Work)

The following artifacts are planned for future phases. They are listed here to fix scope and establish traceability. [Ref: §24]

| Artifact Name | Artifact Class | Authoritative Source | Owner | Generated/Manual | Lifecycle | Phase Introduced |
|---|---|---|---|---|---|---|
| **Lifecycle specification** | Authoritative | §12 (Engineering Lifecycle) | Standard Authority | Manual | Planned | Phase 3 |
| **Artifact catalog** | Authoritative | §11.4 (Full artifact catalog) | Standard Authority | Manual | Planned | Phase 4 |
| **Artifact schemas** | Derived | §11.4, §43 (Object Model) | SES Maintainers | Generated | Planned | Phase 4 |
| **Stage catalog** | Authoritative | §13 (Stage Model) | Standard Authority | Manual | Planned | Phase 5 |
| **Stage specifications** | Authoritative | §13.2 (Mandatory Stage Schema) | Standard Authority | Manual | Planned | Phase 5 |
| **Validation rules** | Authoritative | §16 (Validation Model), VL-1–VL-5 | Standard Authority | Manual | Planned | Phase 6 |
| **Conformance procedure** | Authoritative | §16.5 (Conformance assertion) | Standard Authority | Manual | Planned | Phase 6 |
| **Checklists** | Derived | §16 (Validation), §15 (Review Model), RV-3 | SES Maintainers | Generated | Planned | Phase 6 |
| **Governance procedure** | Authoritative | §17 (Governance Model), GV-1–GV-7 | Standard Authority | Manual | Planned | Phase 7 |
| **RACI matrix** | Derived | §17.2 GV-7 (Roles) | Standard Authority | Manual | Planned | Phase 7 |
| **ADR template** | Derived | §11.3 (ADR), §35.2 (Decision Structure) | SES Maintainers | Generated | Planned | Phase 8 |
| **Contract template** | Derived | §11.3 (Contract), §14.2 (Contracts) | SES Maintainers | Generated | Planned | Phase 8 |
| **Design document template** | Derived | §38 (Documentation Model), DOC-1–DOC-5 | SES Maintainers | Generated | Planned | Phase 8 |
| **Stage template** | Derived | §13.2 (Mandatory Stage Schema) | SES Maintainers | Generated | Planned | Phase 8 |
| **Checklist template** | Derived | §15 (Review Model), §16 (Validation Model) | SES Maintainers | Generated | Planned | Phase 8 |
| **Worked examples (backend)** | Example | §12 (Lifecycle), domain context | SES Maintainers | Manual | Planned | Phase 9 |
| **Worked examples (frontend)** | Example | §12 (Lifecycle), domain context | SES Maintainers | Manual | Planned | Phase 9 |
| **Worked examples (infrastructure)** | Example | §12 (Lifecycle), domain context | SES Maintainers | Manual | Planned | Phase 9 |
| **Worked examples (reverse engineering)** | Example | §30 (Reverse Engineering Architecture) | SES Maintainers | Manual | Planned | Phase 9 |
| **Worked examples (legacy modernization)** | Example | §12 (Lifecycle), §30, domain context | SES Maintainers | Manual | Planned | Phase 9 |
| **Conformance tooling (parsers)** | Generated | §16 (Validation), FR-13, NFR-1 | SES Maintainers | Generated | Planned | Post-standard |
| **Conformance tooling (traceability generators)** | Generated | §48 (Traceability Graph), TGR-4 | SES Maintainers | Generated | Planned | Post-standard |
| **Evidence base verification report** | Generated | Appendix A, RK-6, AS-5 | SES Maintainers | Generated | Planned | Before first MAJOR release |

---

## 4. Registry Rules

### 4.1 Completeness

This registry SHALL contain every artifact that currently exists or is planned in the SES repository. [Ref: §11.4, §24] No artifact SHALL exist in the repository without an entry in this registry. [Ref: §11.2, CON-1]

### 4.2 Authority Class Assignment

Every artifact SHALL be assigned exactly one primary authority class per §11.1: [Ref: §11.1, FR-3]
- **Authoritative** — The single source of truth for some fact or decision.
- **Derived** — Produced by transforming one or more authoritative artifacts.
- **Generated** — Mechanically produced from authoritative sources or from the system under engineering.

### 4.3 Metadata Requirements

Every artifact SHALL carry, at minimum, the following metadata: [Ref: §11.2]

| Field | Value Source |
|---|---|
| Unique identifier | Object ID per §43.2 |
| Authority class | §11.1 |
| Owner | §11.2; §17 GV-7 roles |
| Version | §18 (Semantic Versioning) |
| Status | Draft / Accepted / Superseded / Deprecated per §11.2 |
| Source pointer | For Derived/Generated: authoritative source(s) per §11.2 |

### 4.4 Edit Policy by Class

| Class | Edit Policy |
|---|---|
| Authoritative | MAY be edited by humans through review + governance per §17. [Ref: §11.1] |
| Derived | MUST NOT be hand-edited; MUST be regenerated from source. [Ref: §11.1, FR-3] |
| Generated | MUST NOT be hand-edited; MUST be reproducible. [Ref: §11.1, FR-3] |

### 4.5 Generation Policy

Any derived or generated artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: RA-4] A derived or generated artifact that cannot be regenerated has silently become a second source of truth. [Ref: RA-4, PR-6]

### 4.6 Phase Ordering

Artifact introduction SHALL respect the phase dependency ordering declared in §24: [Ref: §24]

```
Phase 2: Repository structure + this registry
Phase 3: Lifecycle specification
Phase 4: Artifact catalog + schemas + special types
Phase 5: Stage catalog + specifications
Phase 6: Validation rules + conformance procedure + checklists
Phase 7: Governance procedure + RACI
Phase 8: Templates
Phase 9: Worked examples
Post-standard: Conformance tooling
```

---

## 5. Storage Location Mapping

Per §10.3, artifacts SHALL be stored in the repository region corresponding to their supplementary class: [Ref: §10.3]

| Repository Region | Artifact Classes Stored |
|---|---|
| `NORMATIVE STANDARD` | Authoritative artifacts (§3.1) |
| `DERIVED OPERATIONAL DOCS` | Derived artifacts (§3.2) |
| `REFERENCE MATERIAL` | Reference supplementary class (§4.1) |
| `TEMPLATES` | Template supplementary class (§4.2) |
| `EXAMPLES` | Example supplementary class (§4.3) |

[Ref: §10.3 architectural view]

---

## 6. Traceability

This registry traces to the following SDD sections: [Ref: §48]

| Registry Section | Traces to SDD Section |
|---|---|
| §3.1 (Existing artifacts) | §10.3, §11, §24 (Phase 2) |
| §3.2 (Special types) | §11.3, §24 (Phase 4) |
| §3.3 (Planned artifacts) | §24 (Future Work table) |
| §4 (Registry rules) | §11.1, §11.2, §11.4, FR-2, FR-3 |
| §5 (Storage mapping) | §10.3, RA-2 |

---

*End of Artifact Registry. This document is an authoritative artifact per §11.1.*
