# Artifact Catalog

> **Authority Class:** Authoritative
> **SDD Authority:** §11.4, §11.1, §11.2, §11.3, §14.2, §43.2
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document is the master catalog of all artifact types defined by the Software Engineering Standard (SES). It enumerates the artifact authority classes, names each special artifact type and knowledge category artifact, and defines the mandatory metadata schema that every artifact SHALL carry. [Ref: §11.4]

This catalog satisfies FR-2 ("The SES SHALL define a closed set of artifact classes, each with: purpose, authority classification, owner, and lifecycle") and FR-3 ("The SES SHALL classify every artifact as authoritative, derived, or generated"). [Ref: §8 FR-2, FR-3]

## 2. Scope

This document specifies artifact types at the field level. It does NOT provide templates (Phase 8 deliverable), examples (Phase 9 deliverable), or operational procedures (Phase 3, Phase 5, Phase 6 deliverables). [Ref: §11.4; §24]

## 3. Artifact Authority Classes

Every artifact the SES recognizes SHALL be classified into exactly one of three authority classes. [Ref: §11.1]

### 3.1 Authoritative

| Property | Specification |
|---|---|
| **Definition** | The single source of truth for some fact or decision. Hand-authored. [Ref: §11.1] |
| **Editing Rule** | MAY be edited by humans through review and governance. [Ref: §11.1] |
| **Rationale** | Prevents documentation drift by maintaining exactly one authoritative location per fact (PR-6, RA-3). [Ref: §11.1; §10.3 RA-3] |
| **Examples** | The SDD; Architecture Decision Records (ADRs); Contract Specifications; Invariant Registers. [Ref: §11.1] |

### 3.2 Derived

| Property | Specification |
|---|---|
| **Definition** | Produced by transforming one or more authoritative artifacts; carries no independent truth. [Ref: §11.1] |
| **Editing Rule** | MUST NOT be hand-edited; MUST be regenerated from source. [Ref: §11.1] |
| **Rationale** | Ensures derived artifacts remain consistent with their authoritative sources (RA-4). [Ref: §10.4 RA-4] |
| **Examples** | SOP derived from lifecycle; checklists derived from stages. [Ref: §11.1] |

### 3.3 Generated

| Property | Specification |
|---|---|
| **Definition** | Mechanically produced from authoritative sources or from the system under engineering. [Ref: §11.1] |
| **Editing Rule** | MUST NOT be hand-edited; MUST be reproducible. [Ref: §11.1] |
| **Rationale** | Guarantees that mechanical outputs can be deterministically recreated (RA-4). [Ref: §10.4 RA-4] |
| **Examples** | Dependency graphs; API reference from contracts; traceability indexes. [Ref: §11.1] |

### 3.4 Tri-Class Enforcement

- FR-3: The SES SHALL classify every artifact as authoritative, derived, or generated, and SHALL state that generated/derived artifacts MUST NOT be hand-edited. [Ref: §8 FR-3]
- RA-4: Any derived or generated artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: §10.4 RA-4]
- RA-5: The normative standard region is authoritative over all other regions. [Ref: §10.4 RA-5]

## 4. Special Artifact Types

The following five artifact types are recognized as constitutionally important and SHALL be specified in Phase 4. [Ref: §11.3] Each is listed with its authority class and definition as provided by the SDD.

### 4.1 Architecture Decision Record (ADR)

| Property | Specification |
|---|---|
| **Authority Class** | Authoritative [Ref: §11.3] |
| **Definition** | A subtype of Decision (§35.2) recording architecture/engineering choices. [Ref: §11.3; §35.2] |
| **Immutability** | Immutable once accepted; superseded by a new record, never edited. [Ref: §11.3; KN-2] |
| **Evidence basis** | Nygard, 2011 [Ref: §11.3] |

### 4.2 Contract Specification

| Property | Specification |
|---|---|
| **Authority Class** | Authoritative [Ref: §11.3] |
| **Definition** | The agreed interface plus semantics across a boundary. [Ref: §11.3; §14.2] |
| **Evidence basis** | OpenAPI/AsyncAPI/proto formats; Meyer, Design by Contract [Ref: §11.3] |
| **Format constraint** | The SDD references OpenAPI/AsyncAPI/proto as formats but does not mandate any; per CN-1 (vendor/tool independence), the Contract Specification schema SHALL be format-agnostic. [Ref: §11.3; §23 CN-1] |

### 4.3 Invariant Register

| Property | Specification |
|---|---|
| **Authority Class** | Authoritative [Ref: §11.3] |
| **Definition** | The constraints that MUST remain true across changes. [Ref: §11.3; §14.2] |
| **Relationship to integrity rules** | INT-1 through INT-10 (§40.1) are integrity-rule instances that SHALL be recorded in the Invariant Register. [Ref: §40.1] |

### 4.4 Provenance Record

| Property | Specification |
|---|---|
| **Authority Class** | Authoritative [Ref: §11.3] |
| **Definition** | Links any recorded fact to its source evidence. [Ref: §11.3; §14.2] |
| **Evidence basis** | PR-5; ISO/IEC/IEEE 29148 traceability [Ref: §11.3; §14.2] |
| **Knowledge rule** | KN-1: Every recorded fact MUST carry provenance — a reference to the source evidence from which it was derived. A fact without provenance is non-authoritative. [Ref: §14.3 KN-1] |

### 4.5 Traceability Index

| Property | Specification |
|---|---|
| **Authority Class** | Generated [Ref: §11.3] |
| **Definition** | Links principles to requirements to verification. [Ref: §11.3; §48] |
| **Editing Rule** | MUST NOT be hand-edited; MUST be generated. [Ref: §11.1 (Generated class); TRC-3] |
| **Evidence basis** | ISO/IEC/IEEE 29148 [Ref: §11.3] |
| **Normative rule** | TRC-3: Traceability links SHOULD be generated artifacts, not hand-maintained, to prevent drift. [Ref: §29.3 TRC-3] |

## 5. Knowledge Category Artifacts

The SES SHALL recognize six categories of durable engineering knowledge, each an authoritative artifact (§11). [Ref: §14.2] These categories constitute the Knowledge Model and satisfy FR-5 ("The SES SHALL define a knowledge model that records engineering facts, decisions, contracts, and invariants, each with mandatory provenance to source evidence"). [Ref: §8 FR-5]

### 5.1 Facts

| Property | Specification |
|---|---|
| **Definition** | Verified statements about the system, each with provenance. [Ref: §14.2] |
| **Evidence basis** | Chikofsky & Cross (recovered facts); Moose/Rigi fact-extraction tradition [Ref: §14.2] |
| **Mandatory fields** | Every recorded engineering fact SHALL contain: Confidence Level (A–E); Evidence Source; Verification Status; Timestamp; Repository Reference. [Ref: §26.3] |
| **Knowledge rule** | KN-1: Every recorded fact MUST carry provenance. KN-3: A hypothesis MUST be marked as a hypothesis until verified; it MUST NOT be recorded as a fact. KN-6: Where feasible, a fact SHOULD be corroborated by more than one source class before being recorded as authoritative. [Ref: §14.3] |

### 5.2 Decisions

| Property | Specification |
|---|---|
| **Definition** | Architecture/engineering decisions, recorded in ADR format, immutable once accepted. [Ref: §14.2] |
| **Evidence basis** | Nygard, 2011 [Ref: §14.2] |
| **Structure** | A Decision SHALL record: Decision; Decision Context; Alternatives; Evidence; Impact; Dependencies; Approval; Status; Superseded By. [Ref: §35.2] |
| **Knowledge rule** | KN-2: Decisions MUST be recorded in an immutable, append/supersede format. An accepted decision MUST NOT be silently edited; it is superseded by a new record. [Ref: §14.3 KN-2] |
| **Normative rule** | DEC-1: Every engineering decision MUST be recorded with all nine fields. DEC-3: A Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By. [Ref: §35.3] |

### 5.3 Contracts

| Property | Specification |
|---|---|
| **Definition** | Agreed interfaces plus semantics across boundaries. [Ref: §14.2] |
| **Evidence basis** | OpenAPI/AsyncAPI/proto; Meyer (Design by Contract) [Ref: §14.2] |
| **Knowledge rule** | KN-4: Contracts are authoritative and changes to them MUST pass through governance and versioning. [Ref: §14.3 KN-4] |
| **Integrity rule** | INT-4: Every API MUST have a contract. [Ref: §40.1 INT-4] |

### 5.4 Invariants

| Property | Specification |
|---|---|
| **Definition** | Constraints that MUST remain true. [Ref: §14.2] |
| **Evidence basis** | Converged practice — invariants/contracts; Meyer [Ref: §14.2] |
| **Knowledge rule** | KN-4: Invariants are authoritative and changes to them MUST pass through governance and versioning. [Ref: §14.3 KN-4] |
| **Canonical term** | "Constraint" — a non-negotiable boundary (§46.2). [Ref: §46.2] |

### 5.5 Rationale

| Property | Specification |
|---|---|
| **Definition** | Why a decision was made; alternatives considered. [Ref: §14.2] |
| **Evidence basis** | Google design-doc convention; ADR "consequences" [Ref: §14.2] |
| **Relationship to Decision** | Rationale is a component of the Decision structure (§35.2 field "Alternatives" and implicit in "Decision Context"). [Ref: §35.2] |

### 5.6 Provenance

| Property | Specification |
|---|---|
| **Definition** | Link from any fact to its source evidence. [Ref: §14.2] |
| **Evidence basis** | PR-5; ISO/IEC/IEEE 29148 traceability [Ref: §14.2] |
| **Mandatory presence** | Every recorded engineering fact SHALL carry provenance (KN-1). Every evidence item SHALL carry provenance and confidence (INT-10). [Ref: §14.3 KN-1; §40.1 INT-10] |

## 6. Mandatory Metadata Schema

### 6.1 Artifact Metadata (§11.2)

Every artifact SHALL carry, at minimum, the following metadata fields. [Ref: §11.2]

| Field | Meaning | Source |
|---|---|---|
| **Unique identifier** | A unique identifier distinguishing this artifact from all others | §11.2 |
| **Authority class** | One of: Authoritative, Derived, Generated (§11.1) | §11.1, §11.2 |
| **Owner** | Single accountable owner | §11.2 |
| **Version** | Semantic version per §18 | §18 |
| **Status** | Draft / Accepted / Superseded / Deprecated | §11.2 |
| **Pointer to authoritative source(s)** | For derived/generated artifacts: the authoritative source(s) from which the artifact is produced | §11.2 |

Rationale: PR-5 (provenance), PR-6 (single source of truth). [Ref: §11.2]

### 6.2 Generalized Object Fields (§43.2)

The Object Model generalizes §11.2 artifact metadata into fifteen mandatory fields that every engineering object SHALL carry. [Ref: §43.2] Artifacts are objects; therefore every artifact SHALL carry all fifteen fields. [Ref: §43.1; OM-5]

| Field | Meaning | Source |
|---|---|---|
| **Object ID** | Unique identifier | §11.2 |
| **Object Type** | A §42.2 entity | §42 |
| **Authority Class** | Authoritative / Derived / Generated | §11.1 |
| **Owner** | Single accountable owner | §11.2 |
| **Lifecycle State** | Current §33 state | §33 |
| **Status** | Draft / Accepted / Superseded / Deprecated | §11.2 |
| **Version** | Semantic version | §18 |
| **Parent Objects** | Containing/owning objects | §44 (contains/owns) |
| **Child Objects** | Contained objects | §44 |
| **Incoming Relationships** | Edges into the object | §44 |
| **Outgoing Relationships** | Edges out of the object | §44 |
| **Evidence References** | Provenance links | §26, §28 |
| **Decision References** | Authorizing decision(s) | §35 |
| **Repository Location** | Canonical location | §10 |
| **Traceability Links** | Graph node links | §48 |

### 6.3 Object Model Enforcement

- OM-1: Every engineering object MUST carry all fifteen fields (§43.2). [Ref: §43.3 OM-1]
- OM-2: No engineering object MAY exist outside this model. [Ref: §43.3 OM-2]
- OM-3: Object Type MUST be a §42.2 entity; Authority Class MUST be from §11.1. [Ref: §43.3 OM-3]
- OM-5: These fields are a superset of, and consistent with, §11.2 artifact metadata. [Ref: §43.3 OM-5]
- OM-6: Generated/Derived objects MUST remain reproducible; their fields MUST NOT be hand-forged. [Ref: §43.3 OM-6]

## 7. Completion Criteria

This Artifact Catalog document is complete when all of the following hold:

1. All three artifact authority classes from §11.1 are defined with definition, edit policy, and examples.
2. All five special artifact types from §11.3 are listed with authority class and SDD-provided definition.
3. All six knowledge categories from §14.2 are defined with their SDD-provided definitions, evidence bases, and governing rules.
4. The mandatory metadata schema from §11.2 is fully specified.
5. The fifteen mandatory object fields from §43.2 are enumerated and related to §11.2.
6. Every normative statement carries a [Ref: §X.Y] citation.

SDD does not specify a field-level template format for artifact catalog entries. [Ref: §11.4]
