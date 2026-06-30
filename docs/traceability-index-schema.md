# Traceability Index Schema

> **Authority Class:** Generated
> **SDD Authority:** §11.3, §29, §48, Appendix C
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the schema for the **Traceability Index**, a generated artifact that links principles → requirements → verification. [Ref: §11.3] The Traceability Index is the operational realization of the Traceability Expansion model (§29) and the Traceability Graph (§48), scoped to the requirements dimension defined in Appendix C.

The Traceability Index SHALL be a **generated** artifact per §11.1 and §11.3. [Ref: §11.1, §11.3] It MUST NOT be hand-edited; it MUST be regenerated from authoritative sources. [Ref: §11.1, PR-6, RA-4]

## 2. Authority Class (Generated)

**Generated** — The Traceability Index is mechanically produced from authoritative sources (principles, requirements, verification methods, and success criteria). [Ref: §11.1, §11.3] It carries no independent truth. [Ref: §11.1] Any edit to the index without a corresponding change to its authoritative source constitutes documentation drift and is non-conformant. [Ref: P-4, RK-4]

- The Traceability Index MUST be reproducible from its authoritative sources by a documented, tool-agnostic procedure. [Ref: RA-4]
- The index SHALL be classified as Generated per the Artifact Authority Model. [Ref: §11.1]

## 3. Schema Definition

A Traceability Index entry SHALL contain the following structure, derived from Appendix C, §29, and §48.

### 3.1 Index Header

| Field | Cardinality | Description | Source |
|---|---|---|---|
| **Index ID** | 1 | Unique identifier for this index entry | §11.2 (unique identifier) |
| **Index Type** | 1 | Fixed value: `TraceabilityIndex` | §11.3 |
| **Authority Class** | 1 | Fixed value: `Generated` | §11.1 |
| **Generation Source** | 1..* | Pointers to authoritative sources from which this index is produced | §11.2 (pointer to authoritative sources); RA-4 |
| **Generated At** | 1 | ISO 8601 timestamp of generation | §11.2 |
| **Generator Version** | 1 | Semantic version of the generation tool/procedure | §18, VS-1 |
| **Status** | 1 | Current / Stale | §11.2 |

### 3.2 Traceability Link Fields

Each index entry SHALL contain one row of the following traceability matrix, per Appendix C and §29:

| Field | Cardinality | Description | Source |
|---|---|---|---|
| **Requirement ID** | 1 | Identifier of the requirement (FR-n, NFR-n, or other normative rule) | Appendix C; §8; §9 |
| **Principle References** | 1..* | Principle(s) to which the requirement traces | Appendix C; §7; PR-5 |
| **Verification Method** | 1..* | Inspection / Analysis / Demonstration / Test per §16.2 | Appendix C; §16.2; PR-7 |
| **Success Criterion** | 1..* | Success criterion verifying the requirement | Appendix C; §20 |

### 3.3 Bidirectional Trace Fields

Per §29, traceability SHALL be bidirectional. [Ref: §29.3, TRC-1] The index SHALL support:

| Field | Cardinality | Description | Source |
|---|---|---|---|
| **Forward Traces** | 0..* | Links to implementations, tests, documentation derived from this requirement | TRC-2; §29.2 |
| **Backward Traces** | 0..* | Links to principles, evidence, and facts that justify this requirement | TRC-2; §28 |
| **Impact Traces** | 0..* | Links to nodes affected by a change to this requirement | TRC-4 |

## 4. Field Specifications

### 4.1 Requirement ID

The Requirement ID field SHALL contain the unique identifier of a normative requirement defined in the SDD. [Ref: §8, §9] Supported requirement classes include:

- **FR-n** — Functional Requirements [Ref: §8]
- **NFR-n** — Non-Functional Requirements [Ref: §9]
- **PR-n** — Engineering Principles [Ref: §7]
- **OBJ-n** — Objectives [Ref: §3]
- **SC-n** — Success Criteria [Ref: §20]
- **Rule IDs** from architectural models (e.g., DSC-n, EVC-n, ECH-n, TRC-n, etc.) [Ref: §25–§50]

### 4.2 Principle References

The Principle References field SHALL contain one or more principle IDs (PR-n) from §7 that the requirement traces to. [Ref: Appendix C] Every normative rule traces to at least one principle. [Ref: §7]

### 4.3 Verification Method

The Verification Method field SHALL contain one or more methods from the standard taxonomy defined in §16.2. [Ref: §16.2, Appendix C]

| Method | Code | Description |
|---|---|---|
| **Inspection** | I | Formal, rigorous examination against criteria |
| **Analysis** | A | Mathematical, logical, or structured evaluation |
| **Demonstration** | D | Operation showing the requirement is satisfied |
| **Test** | T | Execution against predefined cases and criteria |

Every requirement in the SES SHALL be assigned one or more verification methods. [Ref: §16.2, VL-2]

### 4.4 Success Criterion

The Success Criterion field SHALL contain one or more success criterion IDs (SC-n) from §20 that verify the requirement. [Ref: Appendix C] Each objective in §3 has a corresponding success criterion. [Ref: §20]

### 4.5 Trace Direction Support

The index SHALL support all six trace directions defined in §48.2. [Ref: §48.2, TGR-2]

- **Forward Trace** — from requirement to implementation, test, documentation
- **Backward Trace** — from requirement to principle, evidence, fact
- **Impact Trace** — change propagation to linked nodes [Ref: TRC-4]
- **Dependency Trace** — follows depends_on / requires relationships [Ref: §44.2]
- **Evidence Trace** — follows verified_by links [Ref: §44.2]
- **Decision Trace** — follows implements / approved_by links [Ref: §44.2]

## 5. Generation Rules

### 5.1 Source of Generation

The Traceability Index SHALL be generated from:

1. **Principles** (§7) — the constitutional foundation
2. **Requirements** (§8, §9) — functional and non-functional
3. **Verification methods** (§16.2) — per-requirement verification assignment
4. **Success criteria** (§20) — objective verification of objectives
5. **Relationship Model** (§44) — references and verified_by relationship types [Ref: §44.2]

### 5.2 Generation Procedure

The Traceability Index SHALL be produced by the following procedure:

1. **Extract** all requirement IDs from authoritative sources (§8, §9, §25–§50).
2. **Extract** all principle IDs (§7) to which each requirement traces.
3. **Extract** all verification methods assigned to each requirement (§16.2, Appendix C).
4. **Extract** all success criteria linked to each requirement (§20, Appendix C).
5. **Build** bidirectional links using Relationship Model types `references` and `verified_by`. [Ref: §44.2]
6. **Validate** that every requirement traces to at least one principle and at least one success criterion. [Ref: PR-5, PR-7]
7. **Output** the index as a structured, machine-readable artifact.

### 5.3 Regeneration Triggers

The Traceability Index MUST be regenerated when any of its authoritative sources change. [Ref: RA-4] Specifically:

- A principle is added, modified, or deprecated [Ref: §18]
- A requirement is added, modified, or deprecated [Ref: §18]
- A verification method is reassigned [Ref: §16]
- A success criterion is added or modified [Ref: §20]
- A relationship type changes [Ref: §44]

### 5.4 Traceability Index Rules

- **TRC-1**: The SES SHALL maintain bidirectional traceability across the engineering work chain (§29.2). [Ref: §29.3, TRC-1]
- **TRC-2**: Every engineering decision MUST be traceable backward (evidence/facts) and forward (implementation, test, documentation). [Ref: §29.3, TRC-2]
- **TRC-3**: Traceability links SHOULD be generated artifacts (§11), not hand-maintained, to prevent drift. [Ref: §29.3, TRC-3]
- **TRC-4**: A change to any node MUST be propagable to its linked nodes (change-impact analysis). [Ref: §29.3, TRC-4]
- **TRC-5**: This expands Appendix C from requirement-only to engineering-work traceability. [Ref: §29.3, TRC-5]

## 6. Relationship to Traceability Graph

### 6.1 Graph Architecture

The Traceability Index is a **requirements-scoped view** of the Traceability Graph (§48). [Ref: §48, TGR-5] The Traceability Graph generalizes the index from requirements to all engineering objects. [Ref: §48.1]

### 6.2 Node and Edge Correspondence

| Traceability Index Element | Traceability Graph Element | Source |
|---|---|---|
| Requirement ID | Node in the graph (§43 object) | §48.2, TGR-3 |
| Principle Reference | Node (§42.2 entity: Requirement) | §42.2 |
| Verification Method | Edge attribute (verified_by) | §44.2 |
| Success Criterion | Node (§42.2 entity: Requirement) | §42.2 |
| Forward/Backward Trace | Edge in the graph (§44 relationship) | §48.2, TGR-2 |

- The graph is built from Object nodes (§43) and Relationship edges (§44); it introduces no new node/edge types. [Ref: TGR-3]
- The traceability graph SHOULD be a generated artifact, not hand-maintained. [Ref: TGR-4]
- Appendix C is a requirements-scoped view of this graph and MUST remain consistent with it. [Ref: TGR-5]

### 6.3 Consistency Requirements

The Traceability Index MUST remain consistent with the Traceability Graph. [Ref: TGR-5] Inconsistency between the index and the graph constitutes a CON-4 violation (broken traceability). [Ref: §49, CON-4]

Every engineering object MUST be a node in the traceability graph; no object MAY be orphaned. [Ref: TGR-1] The graph MUST support all six trace directions (§48.2) bidirectionally. [Ref: TGR-2]

## 7. Completion Criteria

This schema is complete when:

1. The index structure captures the principle → requirement → verification → success criterion linkage defined in Appendix C. [Ref: Appendix C]
2. All five Traceability Expansion rules (TRC-1..TRC-5) are satisfied by the schema. [Ref: §29.3]
3. The index is classified as Generated per §11.1 and carries generation metadata per §11.2. [Ref: §11.1, §11.2]
4. Bidirectional traceability is supported per TRC-1 and TGR-2. [Ref: §29.3, §48.3]
5. Relationship types `references` and `verified_by` from §44.2 are incorporated. [Ref: §44.2]
6. The index is reproducible from authoritative sources per RA-4. [Ref: RA-4]
7. The schema does not introduce requirements, fields, or terminology not present in the SDD. [Ref: §11.4]
