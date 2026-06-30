# Architecture Decision Record (ADR) Schema

> **Authority Class:** Authoritative
> **SDD Authority:** §11.3, §35.2, KN-2
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the schema for the Architecture Decision Record (ADR), a special artifact type recognized by the SES as constitutionally important. The ADR is the authoritative format for recording architecture and engineering decisions. It is immutable once accepted and is superseded — never edited — when change is required. [Ref: §11.3; KN-2]

This schema satisfies FR-5 ("The SES SHALL define a knowledge model that records engineering facts, decisions, contracts, and invariants") and FR-2 ("The SES SHALL define a closed set of artifact classes"). [Ref: §8 FR-5, FR-2]

## 2. Authority Class

The ADR is **Authoritative** — the single source of truth for the decision it records. It is hand-authored and MAY be created through review and governance. [Ref: §11.1 (Authoritative class); §11.3]

The ADR is a subtype of Decision (§35.2) and inherits all Decision rules (DEC-1 through DEC-5). [Ref: §35.3 DEC-5]

## 3. Schema Definition

An ADR SHALL contain all nine fields defined in §35.2 plus ADR-specific immutability and supersession rules defined in KN-2 and §11.3. [Ref: §35.2; §11.3; KN-2]

The ADR SHALL carry the mandatory artifact metadata per §11.2 and the fifteen mandatory object fields per §43.2. [Ref: §11.2; §43.2]

### 3.1 Schema Summary

| Field | Required | Source |
|---|---|---|
| Decision | REQUIRED | §35.2 |
| Decision Context | REQUIRED | §35.2 |
| Alternatives | REQUIRED | §35.2 |
| Evidence | REQUIRED | §35.2 |
| Impact | REQUIRED | §35.2 |
| Dependencies | REQUIRED | §35.2 |
| Approval | REQUIRED | §35.2 |
| Status | REQUIRED | §35.2 |
| Superseded By | CONDITIONALLY REQUIRED | §35.2; KN-2 |

### 3.2 ADR-Specific Rules

| Rule | Source |
|---|---|
| Immutable once accepted | §11.3; KN-2; DEC-3 |
| Superseded by a new ADR, never edited | §11.3; KN-2 |
| Every implementation MUST trace back to exactly one ADR | §35.3 DEC-4 |

## 4. Field Specifications

### 4.1 Decision

| Property | Specification |
|---|---|
| **Purpose** | States the decision that was made. |
| **Content** | A clear, unambiguous statement of the chosen option. |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 1: "Decision"). [Ref: §35.2] |

### 4.2 Decision Context

| Property | Specification |
|---|---|
| **Purpose** | Describes the situation, problem, or force that necessitated the decision. |
| **Content** | The engineering context, constraints, and requirements that frame the decision. |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 2: "Decision Context"). [Ref: §35.2] |

### 4.3 Alternatives

| Property | Specification |
|---|---|
| **Purpose** | Enumerates the options considered and explains why each was accepted or rejected. |
| **Content** | A list of alternatives with rationale for rejection of non-chosen options; corresponds to the Rationale knowledge category (§14.2). |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 3: "Alternatives"). [Ref: §35.2; §14.2 (Rationale)] |

### 4.4 Evidence

| Property | Specification |
|---|---|
| **Purpose** | Cites the evidence supporting the decision. |
| **Content** | References to verified facts, confidence levels (§26), and provenance links (§28) that justify the decision. |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 4: "Evidence"). [Ref: §35.2; §35.3 DEC-2] |

### 4.5 Impact

| Property | Specification |
|---|---|
| **Purpose** | Describes the consequences of the decision on the system, architecture, and engineering work. |
| **Content** | Impact analysis spanning the dimensions defined in §36.2: affected components, dependencies, execution flow, database, API, security, tests, documentation, deployment, and validation. |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 5: "Impact"). [Ref: §35.2; §35.3 DEC-2; §36.2] |

### 4.6 Dependencies

| Property | Specification |
|---|---|
| **Purpose** | Identifies other decisions, artifacts, or conditions this decision depends upon. |
| **Content** | References to related ADRs, contracts, invariants, or other authoritative artifacts. |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 6: "Dependencies"). [Ref: §35.2] |

### 4.7 Approval

| Property | Specification |
|---|---|
| **Purpose** | Records who approved the decision and when. |
| **Content** | Approver identity; approval timestamp; review reference per §15. |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 7: "Approval"). [Ref: §35.2; §15] |
| **Governing rule** | RV-1: Every authoritative artifact MUST pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2 RV-1] |

### 4.8 Status

| Property | Specification |
|---|---|
| **Purpose** | Indicates the current state of the decision in its lifecycle. |
| **Allowed values** | Draft / Proposed / Accepted / Rejected / Superseded / Deprecated |
| **Required** | REQUIRED. |
| **Source** | §35.2 (field 8: "Status"). [Ref: §35.2; §11.2 (Status field)] |

### 4.9 Superseded By

| Property | Specification |
|---|---|
| **Purpose** | When a decision is superseded, identifies the new ADR that replaces it. |
| **Content** | Object ID of the superseding ADR. |
| **Required** | CONDITIONALLY REQUIRED — MUST be populated when Status = "Superseded"; MUST be empty otherwise. |
| **Source** | §35.2 (field 9: "Superseded By"). [Ref: §35.2; KN-2; DEC-3] |

## 5. Immutability Rules

The following rules govern the immutability of ADRs once accepted.

- **IM-1** An ADR is immutable once accepted. [Ref: §11.3; KN-2]
- **IM-2** An accepted ADR MUST NOT be silently edited, deleted, or modified in place. [Ref: KN-2; DEC-3]
- **IM-3** The principle of immutability prevents loss of decision rationale (P-2) and ensures that the engineering history remains traceable. [Ref: §2.2 P-2]
- **IM-4** Historical ADRs MUST be retained as Historical Knowledge (§31.2, RKA-3). [Ref: §31.3 RKA-3]
- **IM-5** Immutability applies to the ADR content; the Status field transitions from "Accepted" to "Superseded" are permitted via the supersession mechanism. [Ref: §35.3 DEC-3]

## 6. Supersession Rules

The following rules govern how ADRs are superseded.

- **SS-1** Change to an accepted ADR occurs ONLY by creating a new ADR that sets the superseded ADR's Status to "Superseded" and populates "Superseded By" with the new ADR's Object ID. [Ref: KN-2; DEC-3]
- **SS-2** The superseded ADR MUST be retained as Historical Knowledge; it MUST NOT be deleted. [Ref: RKA-3; REL-4]
- **SS-3** The superseding ADR MUST reference the superseded ADR in its Dependencies field. [Ref: §35.2 (Dependencies field)]
- **SS-4** The superseding ADR MUST pass through the full approval workflow (review per §15, governance per §17) before the superseded ADR's Status may be updated. [Ref: §15 RV-1; §17 GV-3]
- **SS-5** Supersession is the ONLY valid mechanism for changing an accepted ADR. In-place edits, silent replacements, or deletion are non-conformant. [Ref: KN-2; DEC-3]
- **SS-6** The relationship type supersedes (§44.2) applies: directed from new ADR to old ADR; old retained as Historical. [Ref: §44.2 supersedes; REL-4]

## 7. Completion Criteria

This ADR Schema document is complete when all of the following hold:

1. The ADR authority class (Authoritative) is declared and justified. [Ref: §11.3]
2. All nine Decision fields from §35.2 are specified with purpose, content, and required status.
3. ADR-specific immutability rules from §11.3 and KN-2 are defined. [Ref: §11.3; KN-2]
4. Supersession rules from KN-2 and DEC-3 are fully specified. [Ref: KN-2; §35.3 DEC-3]
5. Relationship to Decision model (§35) and Knowledge Model (§14) is stated.
6. Every normative statement carries a [Ref: §X.Y] citation.

SDD does not specify the storage format (e.g., Markdown, YAML, JSON) for ADRs. [Ref: §11.3; §35]
