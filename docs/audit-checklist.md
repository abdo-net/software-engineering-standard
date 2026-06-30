# Audit Checklist

> **Authority Class:** Derived
> **SDD Authority:** §15.1, §15.2, §15.3, §16.5
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the Audit review checklist for the Software Engineering Standard (SES). Audit is an independent conformance check against the standard, applied for conformance assessment and certification. [Ref: §15.1, §16.5]

## 2. Scope

This checklist applies to Audits conducted under the SES Review Model (§15). Audit is an independent, criteria-based examination to verify conformance to the SES, distinct from the human/criteria-based review of Inspection and Technical Review. [Ref: §15.1, §15.3]

SDD does not specify the minimum qualification for an auditor or whether auditors must be external to the project being audited. [Ref: §15.1]

## 3. Normative Rules (RV-1..RV-5)

The following normative rules apply to all review types, including Audit, and MUST be verified as part of every Audit. [Ref: §15.2]

| Rule | Statement | Verification |
|---|---|---|
| **RV-1** | Every authoritative artifact MUST pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2] | Confirm the artifact under audit has passed review before effectiveness. |
| **RV-2** | Changes to the standard itself MUST undergo Inspection. [Ref: §15.2] | Confirm the audit target is not a change to the SES subject being audited. |
| **RV-3** | Review MUST be against explicit, written criteria (checklists/verification criteria), not reviewer preference. [Ref: §15.2] | Confirm this checklist or another written criteria document is the basis for the audit. |
| **RV-4** | Review of work SHOULD be performed by someone other than its sole author where independence adds value. [Ref: §15.2] | Confirm auditor independence from the subject of the audit. |
| **RV-5** | Review outcomes (findings, disposition) MUST be recorded as evidence. [Ref: §15.2] | Confirm an audit record artifact exists and will be retained. |

## 4. Review Target (Conformance and Certification)

Per §15.1 and §16.5, Audit SHALL be applied to verify the following:

| Target | Description | Rationale |
|---|---|---|
| **Project conformance to the SES** | Objective verification that a project satisfies applicable SES requirements at a stated standard version. [Ref: §16.5] | Makes "the standard governs projects" verifiable rather than aspirational. [Ref: §16.5, OBJ-7, FR-15] |
| **Repository Readiness** | Verification that all readiness gates (§41.2) are objectively satisfied. [Ref: §41] | Gates implementation start. [Ref: §41.2] |
| **Integrity Rule Compliance** | Verification that no Engineering Integrity Rule (§40) is violated. [Ref: §40] | Violations render work non-conformant. [Ref: §40.2] |

SDD does not specify additional audit targets beyond project conformance, repository readiness, and integrity rule compliance. [Ref: §15.1, §16.5]

## 5. Checklist

### 5.1 Pre-Audit Readiness

| ID | Item | Source |
|---|---|---|
| AU-P1 | The audit scope MUST be defined: which project, which standard version, which requirements. | Derived from conformance assertion [Ref: §16.5] |
| AU-P2 | The SES version against which conformance is audited MUST be stated. [Ref: VS-3] | §18 VS-3 |
| AU-P3 | The auditor MUST have access to the explicit, written criteria against which the Audit is conducted. [Ref: §15.2 RV-3] | §15.2 |
| AU-P4 | The project being audited MUST have a conformance assertion recorded, or the audit is an initial assessment. [Ref: §16.5] | §16.5 |

### 5.2 Conformance Assertion Verification

Per §16.5, the SES SHALL define a conformance assertion: a recorded, evidenced statement that a project satisfies the applicable SES requirements at a stated standard version. [Ref: §16.5]

| ID | Item | Source |
|---|---|---|
| AU-C1 | The project MUST have a recorded conformance assertion naming the standard version it conforms to. [Ref: §16.5, VS-3] | §16.5, §18 VS-3 |
| AU-C2 | The conformance assertion MUST cite the evidence on which it rests. [Ref: VL-4, PR-5] | §16.4 VL-4 |
| AU-C3 | The conformance assertion MUST be expressed as objective pass/fail against stated criteria, not subjective judgment. [Ref: VL-1] | §16.4 VL-1 |
| AU-C4 | The audit MUST verify that the project's conformance assertion is current and covers all applicable requirements. | Derived from §16.5 |

### 5.3 Validation Evidence Verification

Per §16, validation evidence MUST be recorded and reproducible. [Ref: VL-3]

| ID | Item | Source |
|---|---|---|
| AU-V1 | Validation evidence for the project MUST be recorded. [Ref: VL-3] | §16.4 VL-3 |
| AU-V2 | Validation evidence MUST be reproducible. [Ref: VL-3, PR-9] | §16.4 VL-3, §7 PR-9 |
| AU-V3 | Each requirement class applicable to the project MUST have a defined verification method (Inspection, Analysis, Demonstration, or Test). [Ref: VL-2, §16.2] | §16.4 VL-2, §16.2 |
| AU-V4 | Validation MUST be a responsibility distinct from implementation/execution. [Ref: VL-5, PR-8] | §16.4 VL-5 |

### 5.4 Repository Readiness Gate Verification

Per §41, the audit MUST verify readiness gates if the audit scope includes implementation readiness. [Ref: §41]

| ID | Item | Source |
|---|---|---|
| AU-R1 | "Implementation Ready" MUST NOT be asserted unless all subordinate gates are objectively satisfied. [Ref: RDY-1] | §41.3 RDY-1 |
| AU-R2 | Readiness gates MUST be evidenced (provenance) and recorded. [Ref: RDY-2] | §41.3 RDY-2 |
| AU-R3 | Any INT (§40) violation MUST block "Repository Ready." [Ref: RDY-3] | §41.3 RDY-3 |
| AU-R4 | Readiness is re-evaluated each cycle; prior readiness MUST NOT persist across material change. [Ref: RDY-4] | §41.3 RDY-4 |

### 5.5 Engineering Integrity Rule Verification

Per §40, violation of any INT rule renders affected work non-conformant. [Ref: §40.2]

| ID | Item | Source |
|---|---|---|
| AU-I1 | Every implementation MUST trace to a Decision (no undocumented implementation). [Ref: INT-1] | §40.1 INT-1 |
| AU-I2 | Every decision MUST be recorded (no undocumented decision). [Ref: INT-2] | §40.1 INT-2 |
| AU-I3 | Every dependency MUST be discovered and recorded (no undocumented dependency). [Ref: INT-3] | §40.1 INT-3 |
| AU-I4 | Every API MUST have a contract (no undocumented API). [Ref: INT-4] | §40.1 INT-4 |
| AU-I5 | Every database object MUST be documented (no undocumented database object). [Ref: INT-5] | §40.1 INT-5 |
| AU-I6 | Every configuration item MUST be documented (no undocumented configuration). [Ref: INT-6] | §40.1 INT-6 |
| AU-I7 | Every workflow MUST be documented (no undocumented workflow). [Ref: INT-7] | §40.1 INT-7 |
| AU-I8 | Every security rule MUST be documented (no undocumented security rule). [Ref: INT-8] | §40.1 INT-8 |
| AU-I9 | Every assumption MUST be recorded and marked; it MUST NOT be silently relied upon (no undocumented assumption). [Ref: INT-9] | §40.1 INT-9 |
| AU-I10 | Every evidence item MUST carry provenance and confidence (no undocumented evidence). [Ref: INT-10] | §40.1 INT-10 |

SDD does not specify whether integrity rules may be audited individually or must be audited as a complete set. [Ref: §40]

### 5.6 Consistency Rule Verification

Per §49, consistency invariants are structural integrity rules that render the repository non-conformant if violated. [Ref: §49.2 CON-9]

| ID | Item | Source |
|---|---|---|
| AU-N1 | Every object MUST have at least one valid relationship and a traceability node (no orphan object). [Ref: CON-1] | §49.1 CON-1 |
| AU-N2 | Each fact MUST have exactly one authoritative object (no duplicate authority). [Ref: CON-2] | §49.1 CON-2 |
| AU-N3 | Each object MUST have exactly one Owner (no duplicate ownership). [Ref: CON-3] | §49.1 CON-3 |
| AU-N4 | Every traceability link MUST resolve to an existing node (no broken traceability). [Ref: CON-4] | §49.1 CON-4 |
| AU-N5 | Every depends_on / requires MUST resolve (no broken dependency). [Ref: CON-5] | §49.1 CON-5 |
| AU-N6 | The authority/dependency graph MUST be acyclic (no circular authority). [Ref: CON-6] | §49.1 CON-6 |
| AU-N7 | An object MUST be in exactly one State (no conflicting lifecycle state). [Ref: CON-7] | §49.1 CON-7 |
| AU-N8 | Every relationship MUST be a §44 type with allowed endpoints (no invalid relationship). [Ref: CON-8] | §49.1 CON-8 |

### 5.7 Evidence and Provenance

| ID | Item | Source |
|---|---|---|
| AU-E1 | Every recorded engineering fact MUST carry provenance. [Ref: KN-1, PR-5] | §14.3 KN-1 |
| AU-E2 | Every engineering fact MUST carry a confidence level (A-E). [Ref: EVC-1] | §26.4 EVC-1 |
| AU-E3 | Every fact MUST record all five mandatory fields per §26.3: Confidence Level, Evidence Source, Verification Status, Timestamp, Repository Reference. [Ref: EVC-2] | §26.3, §26.4 EVC-2 |

### 5.8 Audit Independence

| ID | Item | Source |
|---|---|---|
| AU-X1 | The auditor MUST be independent from the project being audited. | Derived from "independent conformance check" [Ref: §15.1] and RV-4 [Ref: §15.2] |
| AU-X2 | The audit MUST be against the standard, not against reviewer preference. [Ref: RV-3] | §15.2 RV-3 |

### 5.9 Review/Validation Separation

| ID | Item | Source |
|---|---|---|
| AU-S1 | The Audit MUST NOT be conflated with validation; review is human/criteria-based examination, validation is objective conformance verification. [Ref: §15.3, PR-8] | §15.3 |
| AU-S2 | The Audit findings MUST be recorded as evidence. [Ref: RV-5] | §15.2 RV-5 |

## 6. Recording Requirements (RV-5)

Per RV-5, every Audit MUST produce an audit record containing: [Ref: §15.2]

| Field | Required | Source |
|---|---|---|
| Audit scope (project, standard version, requirements covered) | MUST | §16.5 |
| Audit date | MUST | RV-5 [Ref: §15.2] |
| Auditor(s) | MUST | RV-5 [Ref: §15.2] |
| Criteria document used (this checklist or other) | MUST | RV-3 [Ref: §15.2] |
| Conformance assertion verified | MUST (if applicable) | §16.5 |
| Readiness gates verified | MUST (if in scope) | §41 |
| Integrity rules verified | MUST (if in scope) | §40 |
| Consistency rules verified | MUST (if in scope) | §49 |
| Findings (conformant / non-conformant per item) | MUST | RV-5 [Ref: §15.2] |
| Overall conformance verdict | MUST | §16.5 |
| Non-conformance items and required remediation | MUST (if non-conformant) | RV-5 [Ref: §15.2] |
| Auditor independence statement | MUST | RV-4 [Ref: §15.2] |

SDD does not specify a mandatory audit record template or storage format. [Ref: §15, §16.5]

## 7. Completion Criteria

An Audit is complete when ALL of the following hold:

| ID | Criterion | Source |
|---|---|---|
| **AUC-1** | All checklist items in §5 applicable to the audit scope have been addressed (checked, not-applicable, or explicitly deferred with rationale). | Derived from RV-3 [Ref: §15.2] |
| **AUC-2** | An audit record per §6 has been produced and stored. [Ref: RV-5, §15.2] | §15.2 RV-5 |
| **AUC-3** | Findings have been dispositioned as conformant or non-conformant against stated criteria. [Ref: VL-1] | §16.4 VL-1 |
| **AUC-4** | Non-conformance items, if any, have been documented with required remediation. | Derived from RV-5 [Ref: §15.2] |
| **AUC-5** | The auditor has recorded an independence statement per RV-4. [Ref: RV-4] | §15.2 RV-4 |
| **AUC-6** | The audit verdict has been expressed as objective pass/fail against stated criteria, not subjective judgment. [Ref: VL-1] | §16.4 VL-1 |

SDD does not specify whether audits must be periodic, event-triggered, or both. [Ref: §15.1, §16.5]

---

*This checklist is a derived artifact per §11.1. It derives authority from §15.1, §15.2, and §16.5 and MUST NOT introduce normative rules independent of the SDD.*
