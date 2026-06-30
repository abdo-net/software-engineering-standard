# Provenance Record Schema

> **Authority Class:** Authoritative
> **SDD Authority:** §11.3, §14.2, §28, §26.3, KN-1
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the schema for the **Provenance Record**, the artifact that links any recorded engineering fact to its source evidence. [Ref: §11.3] Every recorded engineering fact MUST carry provenance, per KN-1. [Ref: §14.3, KN-1] The Provenance Record realizes PR-5 (provenance / traceability) at the artifact level. [Ref: §7, PR-5]

The Provenance Record is an **authoritative** artifact per the Artifact Authority Model. [Ref: §11.1] It SHALL be hand-authored and governed. [Ref: §11.1] It belongs to the **Provenance** knowledge category defined in §14.2. [Ref: §14.2]

## 2. Authority Class

**Authoritative** — The Provenance Record is the single source of truth for the link between a fact and its evidence. [Ref: §11.1, §11.3] It MAY be edited by humans through review and governance. [Ref: §11.1] A Provenance Record MUST NOT be silently modified; changes MUST be versioned and governed per §17 and §18. [Ref: §17, §18, GV-1..GV-5]

## 3. Schema Definition

A Provenance Record SHALL contain the following structure, derived from the Evidence Chain (§28) and the mandatory fact fields (§26.3):

### 3.1 Record Header

| Field | Cardinality | Description | Source |
|---|---|---|---|
| **Record ID** | 1 | Unique identifier for this provenance record | §11.2 (unique identifier requirement) |
| **Fact Reference** | 1 | Pointer to the fact this record provenances | §14.2 (Provenance category definition); KN-1 |
| **Record Type** | 1 | Fixed value: `ProvenanceRecord` | §11.3 |
| **Authority Class** | 1 | Fixed value: `Authoritative` | §11.1 |
| **Status** | 1 | Draft / Accepted / Superseded / Deprecated | §11.2 |
| **Version** | 1 | Semantic version per §18 | §18, VS-1 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |

### 3.2 Evidence Link Fields

| Field | Cardinality | Description | Source |
|---|---|---|---|
| **Confidence Level** | 1 | A–E per §26.2 | §26.3 mandatory field; EVC-1 |
| **Evidence Source** | 1..* | Reference to source evidence (file, trace, schema, commit) | §26.3 mandatory field; KN-1 |
| **Verification Status** | 1 | Unverified / Verified / Rejected | §26.3 mandatory field |
| **Timestamp** | 1 | ISO 8601 timestamp of record creation | §26.3 mandatory field |
| **Repository Reference** | 1 | Canonical repository location of the evidenced fact | §26.3 mandatory field; §10 |

### 3.3 Chain Integrity Fields

| Field | Cardinality | Description | Source |
|---|---|---|---|
| **Upstream Reference** | 0..1 | Link to predecessor in Evidence Chain (§28) | ECH-2 (unbroken chain of custody) |
| **Downstream Reference** | 0..* | Links to successor nodes (Knowledge, Decision, Implementation) | ECH-3 |
| **Chain Position** | 1 | Observation / Evidence / Verification / Fact / Knowledge / Decision / Implementation / Validation / Documentation | §28.2 |
| **Blocking Condition** | 0..1 | Any condition blocking progression per §47.2 | INF-3 |

## 4. Field Specifications

### 4.1 Confidence Level

The Confidence Level field SHALL be graded A–E per §26.2. [Ref: §26.2, §26.3]

| Level | Definition | Relative strength |
|---|---|---|
| **A** | Observed directly at runtime (actual behavior) | Highest |
| **B** | Confirmed by implementation (source code) | High |
| **C** | Confirmed by official documentation | Medium |
| **D** | Derived from multiple independent evidence sources (triangulation / inference) | Medium-low |
| **E** | Engineering hypothesis (unverified) | Lowest |

- A Level-E fact is a hypothesis and MUST NOT be treated as authoritative. [Ref: EVC-3, KN-3]
- Confidence MAY be raised only by recording additional evidence/provenance; it MUST NOT be raised by assertion. [Ref: EVC-5]
- No fact MAY become authoritative without a confidence classification. [Ref: EVC-4]

### 4.2 Evidence Source

The Evidence Source field SHALL contain one or more references to the source evidence from which the fact was derived. [Ref: §26.3, KN-1] A fact without provenance is non-authoritative. [Ref: KN-1] Evidence Source SHALL support the following reference types:

- **File reference** — path to a version-controlled file
- **Trace reference** — identifier of a trace in the Traceability Graph (§48)
- **Schema reference** — identifier of a contract/schema artifact
- **Commit reference** — version control commit hash

### 4.3 Verification Status

The Verification Status field SHALL indicate the state of evidence verification:

- **Unverified** — evidence recorded but not yet verified
- **Verified** — evidence has passed the Verification link of the Evidence Chain [Ref: §28.2, ECH-1]
- **Rejected** — evidence failed verification; the associated fact MUST NOT progress to Knowledge [Ref: ECH-5, INF-3]

### 4.4 Timestamp

The Timestamp field SHALL contain an ISO 8601 timestamp indicating when the provenance record was created. [Ref: §26.3] This field supports chain-of-custody audit per NIST SP 800-86. [Ref: §26.3 evidence base]

### 4.5 Repository Reference

The Repository Reference field SHALL contain the canonical location of the evidenced fact within the repository. [Ref: §26.3, §10] This field realizes "repository as permanent memory" (PR-4). [Ref: §7, PR-4]

## 5. Relationship to Evidence Chain

The Provenance Record is the **mechanism by which the Evidence Chain (§28) is made concrete and auditable**. [Ref: §28]

### 5.1 Chain Linkage

The Evidence Chain defines the ordered, provenance-preserving path: [Ref: §28.2]

```
Unknown Observation → Evidence → Verification → Engineering Fact → Knowledge
→ Architecture → Decision → Implementation → Validation → Documentation → Maintenance
```

Each arrow is a provenance link; the downstream node MUST be justified by the upstream node. [Ref: §28.2] The Provenance Record SHALL document each link with:

- **ECH-1**: An observation MUST NOT be recorded as an engineering fact without passing Evidence → Verification. [Ref: §28.3, ECH-1]
- **ECH-2**: Each link MUST preserve provenance to its predecessor (unbroken chain of custody). [Ref: §28.3, ECH-2]
- **ECH-3**: Every Decision MUST trace backward to verified facts and forward to Implementation, Validation, and Documentation. [Ref: §28.3, ECH-3]
- **ECH-4**: Asserting a downstream node without its upstream evidence (a broken chain) is non-conformant. [Ref: §28.3, ECH-4]
- **ECH-5**: Hypotheses (confidence E, §26) MUST NOT pass the Verification link until verified. [Ref: §28.3, ECH-5]

### 5.2 Chain Integrity

The Provenance Record SHALL maintain referential integrity with the Evidence Chain. [Ref: §49, CON-4] Every traceability link MUST resolve to an existing node. [Ref: CON-4] No orphan provenance record MAY exist. [Ref: CON-1]

## 6. Completion Criteria

This schema is complete when:

1. All fields defined in §26.3 (Confidence Level, Evidence Source, Verification Status, Timestamp, Repository Reference) are specified with their cardinality, type, and normative rules. [Ref: §26.3]
2. The five Evidence Chain rules (ECH-1..ECH-5) are mapped to record fields. [Ref: §28.3]
3. KN-1 (every recorded fact MUST carry provenance) is satisfied by the schema structure. [Ref: §14.3, KN-1]
4. The record carries mandatory artifact metadata per §11.2 (identifier, authority class, owner, version, status). [Ref: §11.2]
5. The Confidence Level field conforms to §26.2 (A–E grading). [Ref: §26.2, EVC-1..EVC-6]
6. The schema does not introduce requirements, fields, or terminology not present in the SDD. [Ref: §11.4]
