# Invariant Register Schema

> **Authority Class:** Authoritative
> **SDD Authority:** §11.3, §14.2, §40.1
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the schema for the Invariant Register, a special artifact type recognized by the SES as constitutionally important. The Invariant Register records constraints that MUST remain true across changes to the system, its architecture, and its documentation. [Ref: §11.3; §14.2]

This schema satisfies FR-5 ("The SES SHALL define a knowledge model that records engineering facts, decisions, contracts, and invariants") and FR-2 ("The SES SHALL define a closed set of artifact classes"). [Ref: §8 FR-5, FR-2]

## 2. Authority Class

The Invariant Register is **Authoritative** — the single source of truth for the constraints it records. It is hand-authored and MAY be edited through review and governance. Changes to invariants MUST pass through governance and versioning (KN-4). [Ref: §11.1 (Authoritative class); §11.3; §14.3 KN-4]

## 3. Schema Definition

An Invariant Register SHALL contain, at minimum, a collection of invariant entries, each recording a single constraint that MUST remain true. The register itself SHALL carry the mandatory artifact metadata per §11.2 and the fifteen mandatory object fields per §43.2. [Ref: §11.2; §43.2]

### 3.1 Invariant Entry Schema

Each entry in the Invariant Register SHALL contain, at minimum:

| Field | Required | Source |
|---|---|---|
| Invariant Identifier | REQUIRED | §43.2 (Object ID); §11.2 |
| Invariant Statement | REQUIRED | §11.3 ("constraints that MUST remain true"); §14.2 |
| Scope | REQUIRED | §11.3; §40.1 |
| Authority Class | REQUIRED | §11.2; §43.2 |
| Owner | REQUIRED | §11.2; §43.2 |
| Version | REQUIRED | §11.2; §18; §43.2 |
| Status | REQUIRED | §11.2; §43.2 |
| Governance Record | REQUIRED | §14.2 KN-4; §17 |
| Evidence References | REQUIRED | §43.2; §26; §28 |
| Traceability Links | REQUIRED | §43.2; §48 |

### 3.2 Register-Level Schema

The Invariant Register as a whole SHALL contain:

| Field | Required | Source |
|---|---|---|
| Register Identifier | REQUIRED | §43.2 (Object ID); §11.2 |
| Register Title | REQUIRED | §11.2 (unique identifier semantics) |
| Authority Class | REQUIRED | §11.2; §43.2 |
| Owner | REQUIRED | §11.2; §43.2 |
| Version | REQUIRED | §11.2; §18; §43.2 |
| Status | REQUIRED | §11.2; §43.2 |
| Invariant Entries | REQUIRED | §11.3; §14.2 |
| Traceability Links | REQUIRED | §43.2; §48 |

## 4. Field Specifications

### 4.1 Invariant Identifier

| Property | Specification |
|---|---|
| **Purpose** | Uniquely identifies the invariant entry within the register. |
| **Content** | A unique Object ID conforming to §43.2. |
| **Required** | REQUIRED. |
| **Source** | §43.2 (Object ID); §11.2 (unique identifier). [Ref: §43.2; §11.2] |

### 4.2 Invariant Statement

| Property | Specification |
|---|---|
| **Purpose** | States the constraint that MUST remain true. |
| **Content** | A declarative, verifiable statement of the constraint, phrased such that it evaluates to true or false against the system state. |
| **Required** | REQUIRED. |
| **Source** | §11.3 ("the constraints that MUST remain true"); §14.2 ("Constraints that MUST remain true"). [Ref: §11.3; §14.2] |

### 4.3 Scope

| Property | Specification |
|---|---|
| **Purpose** | Defines the boundary within which the invariant applies. |
| **Content** | Identification of the system, module, component, or boundary to which the invariant is bound. |
| **Required** | REQUIRED. |
| **Source** | §11.3; §40.1 (each INT rule names a scoped artifact type). [Ref: §11.3; §40.1] |

### 4.4 Authority Class

| Property | Specification |
|---|---|
| **Purpose** | Declares the artifact's authority class. |
| **Value** | "Authoritative" for all Invariant Register entries. [Ref: §11.3; §11.1] |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Authority Class). [Ref: §11.2; §43.2] |

### 4.5 Owner

| Property | Specification |
|---|---|
| **Purpose** | Identifies the single accountable owner. |
| **Content** | The person or team responsible for the invariant. |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Owner). [Ref: §11.2; §43.2] |
| **Constraint** | Exactly one Owner per object (CON-3). [Ref: §49.1 CON-3] |

### 4.6 Version

| Property | Specification |
|---|---|
| **Purpose** | Identifies the version of the invariant entry. |
| **Content** | Semantic version per §18 (MAJOR.MINOR.PATCH). [Ref: §18] |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Version). [Ref: §11.2; §43.2] |

### 4.7 Status

| Property | Specification |
|---|---|
| **Purpose** | Indicates the current lifecycle state of the invariant entry. |
| **Allowed values** | Draft / Accepted / Superseded / Deprecated |
| **Required** | REQUIRED. |
| **Source** | §11.2; §43.2 (Status). [Ref: §11.2; §43.2] |

### 4.8 Governance Record

| Property | Specification |
|---|---|
| **Purpose** | Records the governance history of the invariant. |
| **Content** | References to the decision(s) that authorized the invariant, review records per §15, and change history per §18 VS-2. |
| **Required** | REQUIRED. |
| **Source** | §14.2 KN-4 ("Invariants are authoritative and changes to them MUST pass through governance and versioning"); §17. [Ref: §14.3 KN-4; §17] |

### 4.9 Evidence References

| Property | Specification |
|---|---|
| **Purpose** | Links the invariant to the evidence that justifies it. |
| **Content** | Provenance links per §28; confidence levels per §26. |
| **Required** | REQUIRED. |
| **Source** | §43.2 (Evidence References); §26; §28. [Ref: §43.2; §26; §28] |

### 4.10 Traceability Links

| Property | Specification |
|---|---|
| **Purpose** | Links the invariant to related engineering objects in the traceability graph. |
| **Content** | References to the artifacts, components, decisions, and contracts bound by this invariant. |
| **Required** | REQUIRED. |
| **Source** | §43.2 (Traceability Links); §48. [Ref: §43.2; §48] |

## 5. Relationship to Integrity Rules

The Engineering Integrity Rules (§40.1) define ten constitutional completeness invariants (INT-1 through INT-10) that make the standard executable. [Ref: §40.1] Each INT rule is an invariant that SHALL be recorded in the Invariant Register.

### 5.1 Integrity Rules as Invariant Entries

The following INT rules SHALL be represented as entries in the Invariant Register:

| ID | Invariant Statement | Scope |
|---|---|---|
| **INT-1** | No undocumented implementation. Every implementation MUST trace to a Decision (§35) and documentation (§38). | Implementation artifacts |
| **INT-2** | No undocumented decision. Every decision MUST be recorded (§35). | Decision records |
| **INT-3** | No undocumented dependency. Every dependency MUST be discovered (§25) and recorded. | Dependency artifacts |
| **INT-4** | No undocumented API. Every API MUST have a contract (§11.3). | API definitions |
| **INT-5** | No undocumented database object. | Database schemas/objects |
| **INT-6** | No undocumented configuration. | Configuration items |
| **INT-7** | No undocumented workflow. | Workflow definitions |
| **INT-8** | No undocumented security rule. | Security policies/rules |
| **INT-9** | No undocumented assumption. Every assumption MUST be recorded (per §22 pattern) and marked; it MUST NOT be silently relied upon. | Assumption records |
| **INT-10** | No undocumented evidence. Every evidence item MUST carry provenance (§28) and confidence (§26). | Evidence records |

### 5.2 Enforcement

- §40.2: Violation of any INT rule renders the affected work non-conformant (§16), MUST block state transition (STA-2), and MUST block Repository Readiness (§41). [Ref: §40.2]
- INT rules MAY be waived only through governance (§17). [Ref: §40.2]
- STA-5: An INT violation MUST block the transition out of its originating state. [Ref: §33.4 STA-5]
- RDY-3: Any INT violation MUST block "Repository Ready." [Ref: §41.3 RDY-3]

### 5.3 Canonical Vocabulary

- §46.2 defines "Constraint" as canonical term: "A non-negotiable boundary." [Ref: §46.2]
- §46.2 defines "Invariant" (via Appendix B) as: "A constraint that must remain true across changes." [Ref: Appendix B; §46]
- VOC-1: The §46.2 terms are canonical; no later document MAY redefine them. [Ref: §46.3 VOC-1]
- The Invariant Register entries are instances of the "Constraint" canonical term. [Ref: §46.2]

## 6. Completion Criteria

This Invariant Register Schema document is complete when all of the following hold:

1. The Invariant Register authority class (Authoritative) is declared and justified. [Ref: §11.3]
2. The per-entry schema is defined with all mandatory fields specified. [Ref: §11.2; §43.2]
3. The register-level schema is defined. [Ref: §11.3]
4. All ten integrity rules (INT-1 through INT-10) from §40.1 are enumerated as required invariant entries. [Ref: §40.1]
5. Enforcement rules linking INT violations to state transitions and readiness are stated. [Ref: §40.2; STA-5; RDY-3]
6. Canonical vocabulary from §46.2 is cited. [Ref: §46.2]
7. Every normative statement carries a [Ref: §X.Y] citation.

SDD does not specify the storage format or template syntax for Invariant Registers. [Ref: §11.3]
