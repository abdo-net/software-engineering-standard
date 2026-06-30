# Contract Specification Schema

> **Authority Class:** Authoritative
> **SDD Authority:** §11.3, §14.2, §37.2, §46.2
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the schema for the Contract Specification, a special artifact type recognized by the SES as constitutionally important. A Contract Specification is the agreed interface plus semantics across a boundary. It is an authoritative artifact; changes to it MUST pass through governance and versioning. [Ref: §11.3; §14.2 KN-4]

This schema satisfies FR-5 ("The SES SHALL define a knowledge model that records engineering facts, decisions, contracts, and invariants") and FR-2 ("The SES SHALL define a closed set of artifact classes"). [Ref: §8 FR-5, FR-2]

## 2. Authority Class

The Contract Specification is **Authoritative** — the single source of truth for the interface and semantics it defines. It is hand-authored and MAY be edited through review and governance. [Ref: §11.1 (Authoritative class); §11.3]

## 3. Schema Definition

A Contract Specification SHALL record the agreed interface and its semantics across a boundary. The SDD references OpenAPI/AsyncAPI/proto as recognized contract formats but does not mandate any specific format. [Ref: §11.3; §14.2] Per CN-1 (vendor/tool independence), the Contract Specification schema defined herein is format-agnostic. [Ref: §23 CN-1]

### 3.1 Format Independence

- CN-1: The standard MUST be vendor-, tool-, language-, framework-, technology-, and AI-independent. [Ref: §23 CN-1]
- FR-16: The SES core MUST NOT contain any rule that names a specific commercial product, programming language, framework, or AI model as a requirement. [Ref: §8 FR-16]
- The Contract Specification schema SHALL be expressible in any contract-description format (e.g., OpenAPI, AsyncAPI, Protocol Buffers IDL, or plain-text structured form) provided the mandatory fields defined below are present. [Ref: §11.3]

### 3.2 Schema Summary

The Contract Specification SHALL contain, at minimum, the following fields:

| Field | Required | Source |
|---|---|---|
| Contract Identifier | REQUIRED | §11.2 (unique identifier); §43.2 (Object ID) |
| Boundary Definition | REQUIRED | §11.3 ("across a boundary"); §14.2 |
| Interface Specification | REQUIRED | §11.3 ("agreed interface"); §14.2 |
| Semantics Specification | REQUIRED | §11.3 ("semantics"); §14.2 |
| Authority Class | REQUIRED | §11.2; §43.2 |
| Owner | REQUIRED | §11.2; §43.2 |
| Version | REQUIRED | §11.2; §18; §43.2 |
| Status | REQUIRED | §11.2; §43.2 |
| Governance Record | REQUIRED | §14.2 KN-4; §17 |
| Evidence References | REQUIRED | §11.2; §43.2; §26; §28 |
| Traceability Links | REQUIRED | §43.2; §48 |

## 4. Field Specifications

### 4.1 Contract Identifier

| Property | Specification |
|---|---|
| **Purpose** | Uniquely identifies the contract specification within the repository. |
| **Content** | A unique Object ID conforming to §43.2. |
| **Required** | REQUIRED. |
| **Source** | §43.2 (Object ID); §11.2 (unique identifier). [Ref: §43.2; §11.2] |

### 4.2 Boundary Definition

| Property | Specification |
|---|---|
| **Purpose** | Defines the boundary across which the contract applies. |
| **Content** | Identification of the systems, modules, services, or components on either side of the boundary (e.g., API consumer/provider, service A/service B, frontend/backend). |
| **Required** | REQUIRED. |
| **Source** | §11.3 ("across a boundary"); §14.2 ("across boundaries"). [Ref: §11.3; §14.2] |

### 4.3 Interface Specification

| Property | Specification |
|---|---|
| **Purpose** | Defines the syntactic and structural interface. |
| **Content** | The interface definition — endpoints, operations, message types, parameters, data structures, transport protocol, and serialization format. |
| **Required** | REQUIRED. |
| **Source** | §11.3 ("agreed interface"); §14.2. [Ref: §11.3; §14.2] |
| **Format note** | MAY be expressed in OpenAPI, AsyncAPI, Protocol Buffers IDL, or any plain-text structured form. The schema does not mandate a format. [Ref: §11.3; CN-1] |

### 4.4 Semantics Specification

| Property | Specification |
|---|---|
| **Purpose** | Defines the meaning and behavior of the interface — not merely its syntax. |
| **Content** | Pre-conditions, post-conditions, invariants, error behavior, side effects, ordering constraints, idempotency guarantees, and any semantic constraints that MUST hold. |
| **Required** | REQUIRED. |
| **Source** | §11.3 ("semantics"); §14.2; Meyer (Design by Contract). [Ref: §11.3; §14.2] |
| **Design by Contract** | The semantics specification SHALL include pre-conditions and post-conditions consistent with Meyer, Design by Contract. [Ref: §11.3; §14.2; §34.1] |

### 4.5 Authority Class

| Property | Specification |
|---|---|
| **Purpose** | Declares the artifact's authority class. |
| **Value** | "Authoritative" for all Contract Specifications. [Ref: §11.3; §11.1] |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Authority Class). [Ref: §11.2; §43.2] |

### 4.6 Owner

| Property | Specification |
|---|---|
| **Purpose** | Identifies the single accountable owner. |
| **Content** | The person or team responsible for the contract. |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Owner). [Ref: §11.2; §43.2] |
| **Constraint** | Exactly one Owner per object (CON-3). [Ref: §49.1 CON-3] |

### 4.7 Version

| Property | Specification |
|---|---|
| **Purpose** | Identifies the version of the contract. |
| **Content** | Semantic version per §18 (MAJOR.MINOR.PATCH). [Ref: §18] |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Version). [Ref: §11.2; §43.2] |

### 4.8 Status

| Property | Specification |
|---|---|
| **Purpose** | Indicates the current lifecycle state of the contract. |
| **Allowed values** | Draft / Accepted / Superseded / Deprecated |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Status). [Ref: §11.2; §43.2] |

### 4.9 Governance Record

| Property | Specification |
|---|---|
| **Purpose** | Records the governance history of the contract. |
| **Content** | References to the decision(s) that authorized the contract, review records per §15, and change history per §18 VS-2. |
| **Required** | REQUIRED. |
| **Source** | §14.2 KN-4 ("changes to them MUST pass through governance and versioning"); §17. [Ref: §14.3 KN-4; §17] |

### 4.10 Evidence References

| Property | Specification |
|---|---|
| **Purpose** | Links the contract to the evidence that justifies it. |
| **Content** | Provenance links per §28; confidence levels per §26. |
| **Required** | REQUIRED. |
| **Source** | §43.2 (Evidence References); §26; §28. [Ref: §43.2; §26; §28] |

### 4.11 Traceability Links

| Property | Specification |
|---|---|
| **Purpose** | Links the contract to related engineering objects in the traceability graph. |
| **Content** | References to implementations, tests, documentation, and decisions that depend upon or realize this contract. |
| **Required** | REQUIRED. |
| **Source** | §43.2 (Traceability Links); §48. [Ref: §43.2; §48] |

## 5. Comparison Requirements

The Engineering Comparison Model (§37) requires that contracts be subject to objective comparison with their implementations.

### 5.1 Implementation vs Contract Comparison

- §37.2: The model SHALL support comparison between "Implementation vs Contract." [Ref: §37.2]
- CPM-1: Every comparison MUST produce engineering evidence (differences with provenance), never subjective judgment. [Ref: §37.3 CPM-1]
- CPM-2: Comparison results MUST be assigned a confidence level; Runtime-vs-Source disagreements follow EVC-6. [Ref: §37.3 CPM-2]
- CPM-3: Divergences MUST be recorded as findings and MAY raise Decisions or Risks; they MUST NOT be silently reconciled. [Ref: §37.3 CPM-3]

### 5.2 Integrity Rules Applicable to Contracts

- INT-4: Every API MUST have a contract. [Ref: §40.1 INT-4]
- INT-5: Every database object MUST be documented. [Ref: §40.1 INT-5]
- INT-6: Every configuration item MUST be documented. [Ref: §40.1 INT-6]
- INT-8: Every security rule MUST be documented. [Ref: §40.1 INT-8]

### 5.3 Canonical Vocabulary

- §46.2 defines "Contract" as canonical term: "An agreed interface plus its semantics across a boundary." [Ref: §46.2]
- Forbidden synonyms: none explicitly listed for "Contract" in §46.2; the term is Normative. [Ref: §46.2]
- VOC-1: The §46.2 terms are canonical; no later document MAY redefine them. [Ref: §46.3 VOC-1]

## 6. Completion Criteria

This Contract Specification Schema document is complete when all of the following hold:

1. The Contract Specification authority class (Authoritative) is declared and justified. [Ref: §11.3]
2. The format-agnostic schema is defined, satisfying CN-1 (vendor/tool independence). [Ref: §23 CN-1]
3. All mandatory fields are specified with purpose, content description, and required status.
4. Comparison requirements from §37.2 are stated. [Ref: §37.2]
5. Applicable integrity rules from §40.1 are referenced. [Ref: §40.1]
6. Canonical vocabulary from §46.2 is cited. [Ref: §46.2]
7. Every normative statement carries a [Ref: §X.Y] citation.

SDD does not specify a storage format or template syntax for Contract Specifications. [Ref: §11.3]
