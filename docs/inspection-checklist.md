# Inspection Checklist

> **Authority Class:** Derived
> **SDD Authority:** §15.1, §15.2, §15.3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the Inspection review checklist for the Software Engineering Standard (SES). Inspection is the most rigorous review type per IEEE Std 1028-2008, applied to gating high-risk artifacts. [Ref: §15.1]

## 2. Scope

This checklist applies to Inspection reviews conducted under the SES Review Model (§15). Inspection is a formal, rigorous defect-detection activity conducted against explicit written criteria. [Ref: §15.1]

## 3. Normative Rules (RV-1..RV-5)

The following normative rules apply to all review types, including Inspection, and MUST be verified as part of every Inspection. [Ref: §15.2]

| Rule | Statement | Verification |
|---|---|---|
| **RV-1** | Every authoritative artifact MUST pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2] | Confirm the artifact under inspection has not been previously declared effective without review. |
| **RV-2** | Changes to the standard itself MUST undergo Inspection. [Ref: §15.2] | Confirm that if the artifact is a change to the SES, it is subject to Inspection (not a lighter review type). |
| **RV-3** | Review MUST be against explicit, written criteria (checklists/verification criteria), not reviewer preference. [Ref: §15.2] | Confirm this checklist or another written criteria document is the basis for the inspection. |
| **RV-4** | Review of work SHOULD be performed by someone other than its sole author where independence adds value. [Ref: §15.2] | Confirm reviewer independence from the artifact's sole authorship. |
| **RV-5** | Review outcomes (findings, disposition) MUST be recorded as evidence. [Ref: §15.2] | Confirm a review record artifact exists and will be retained. |

## 4. Review Target (High-Risk Artifacts)

Per §15.1, Inspection SHALL gate the following high-risk artifact categories:

| Category | Authority Class | Rationale |
|---|---|---|
| **Contracts** | Authoritative [Ref: §11.3] | Contracts define agreed interfaces and semantics across boundaries; defects have systemic impact. [Ref: §11.3] |
| **Architecture Decision Records (ADRs)** | Authoritative; immutable once accepted [Ref: §11.3, KN-2] | ADRs govern architectural direction; errors are costly to reverse. [Ref: §11.3] |
| **The Standard Itself (the SES)** | Authoritative [Ref: §10.4] | The SES is superordinate to all projects; its correctness governs all conformance. [Ref: §1.2, §15.2 RV-2] |

SDD does not specify additional high-risk artifact categories beyond contracts, ADRs, and the standard itself for Inspection gating. [Ref: §15.1]

## 5. Checklist

### 5.1 Pre-Inspection Readiness

| ID | Item | Source |
|---|---|---|
| IN-P1 | The artifact under review MUST be in a stable, readable state (not actively being edited). | SDD does not specify pre-inspection readiness conditions. [Ref: §15] |
| IN-P2 | The artifact MUST carry mandatory artifact metadata per §11.2: unique identifier, authority class, owner, version, status. [Ref: §11.2] | §11.2 |
| IN-P3 | Reviewers MUST have access to the explicit, written criteria against which inspection is conducted. [Ref: §15.2 RV-3] | §15.2 |
| IN-P4 | Where the artifact is a change to an existing artifact, the diff or change description MUST be available. | SDD does not specify change-review procedures. [Ref: §15] |

### 5.2 Artifact Authority and Metadata

| ID | Item | Source |
|---|---|---|
| IN-A1 | The artifact MUST declare its authority class (authoritative / derived / generated). [Ref: §11.1] | §11.1 |
| IN-A2 | If the artifact is derived or generated, it MUST declare the authoritative source(s) from which it is produced and MUST NOT be hand-edited. [Ref: §11.1, PR-6] | §11.1 |
| IN-A3 | The artifact MUST carry a version identifier consistent with the SES versioning strategy (§18). [Ref: §11.2] | §11.2, §18 |

### 5.3 Evidence and Provenance

| ID | Item | Source |
|---|---|---|
| IN-E1 | Every normative rule in the artifact MUST carry an evidence reference or an explicit UNSUPPORTED marker. [Ref: FR-11, PR-1] | §8 FR-11, §7 PR-1 |
| IN-E2 | Every recorded fact MUST carry provenance linking it to source evidence. [Ref: KN-1, PR-5] | §14.3 KN-1 |
| IN-E3 | Hypotheses MUST be marked as hypotheses and MUST NOT be presented as verified facts. [Ref: KN-3] | §14.3 KN-3 |
| IN-E4 | Decisions, if present, MUST cite the evidence and impact analysis that justify them. [Ref: DEC-2, §35.2] | §35.2, §35.3 DEC-2 |

### 5.4 Integrity and Conformance

| ID | Item | Source |
|---|---|---|
| IN-I1 | The artifact MUST NOT introduce a normative rule that contradicts an existing SES rule. [Ref: NFR-11] | §9 NFR-11 |
| IN-I2 | The artifact MUST NOT name or require a specific commercial product, programming language, framework, or AI model (FR-16). [Ref: FR-16, PR-3] | §8 FR-16, §7 PR-3 |
| IN-I3 | The artifact MUST use RFC 2119 keywords (MUST, MUST NOT, SHALL, SHOULD, MAY) consistently. [Ref: §46, NFR-4] | §46, §9 NFR-4 |
| IN-I4 | The artifact MUST NOT silently edit an accepted ADR; supersession MUST use a new record. [Ref: KN-2, §11.3] | §14.3 KN-2, §11.3 |

### 5.5 Specific Criteria for High-Risk Artifact Types

#### 5.5.1 Contract Specifications

| ID | Item | Source |
|---|---|---|
| IN-C1 | The contract MUST define the agreed interface and semantics across the boundary. [Ref: §11.3] | §11.3 |
| IN-C2 | The contract MUST be classified as authoritative. [Ref: §11.3] | §11.3 |

SDD does not specify detailed contract inspection criteria; full specification is a Phase-4 deliverable. [Ref: §11.4]

#### 5.5.2 Architecture Decision Records (ADRs)

| ID | Item | Source |
|---|---|---|
| IN-D1 | The ADR MUST be classified as authoritative and immutable once accepted. [Ref: §11.3, KN-2] | §11.3, §14.3 KN-2 |
| IN-D2 | The ADR MUST record: Decision, Decision Context, Alternatives, Evidence, Impact, Dependencies, Approval, Status, and Superseded By per §35.2. [Ref: DEC-1] | §35.2, §35.3 DEC-1 |
| IN-D3 | The ADR MUST cite the evidence and impact analysis that justify the decision. [Ref: DEC-2] | §35.3 DEC-2 |

#### 5.5.3 Changes to the Standard Itself

| ID | Item | Source |
|---|---|---|
| IN-S1 | The change MUST NOT be a project-local modification; projects MUST NOT modify the core standard. [Ref: GV-1] | §17.2 GV-1 |
| IN-S2 | The change MUST originate as a proposal containing: the problem, the evidence, the proposed change, the impact on existing requirements, and the affected versions. [Ref: GV-2] | §17.2 GV-2 |
| IN-S3 | The change MUST be supported by evidence from the approved evidence base (Appendix A) or be explicitly marked UNSUPPORTED. [Ref: GV-4, PR-1] | §17.2 GV-4 |
| IN-S4 | The change MUST include a version increment (§18 VS-1) and a changelog entry (§18 VS-2). [Ref: GV-5] | §17.2 GV-5, §18 VS-1, VS-2 |

### 5.6 Review/Validation Separation

| ID | Item | Source |
|---|---|---|
| IN-V1 | The Inspection MUST NOT be conflated with validation; review is human/criteria-based examination, validation is objective conformance verification. [Ref: §15.3, PR-8] | §15.3 |

## 6. Recording Requirements (RV-5)

Per RV-5, every Inspection MUST produce a review record containing: [Ref: §15.2]

| Field | Required | Source |
|---|---|---|
| Artifact identifier | MUST | §11.2 |
| Artifact version reviewed | MUST | §11.2 |
| Review date | MUST | RV-5 [Ref: §15.2] |
| Reviewer(s) | MUST | RV-5 [Ref: §15.2] |
| Criteria document used (this checklist or other) | MUST | RV-3 [Ref: §15.2] |
| Findings (defects, questions, observations) | MUST | RV-5 [Ref: §15.2] |
| Disposition (pass / fail / conditional pass) | MUST | RV-5 [Ref: §15.2] |
| Required rework items, if any | MUST (if fail or conditional) | RV-5 [Ref: §15.2] |
| Evidence of reviewer independence (RV-4) | SHOULD | RV-4 [Ref: §15.2] |

SDD does not specify a mandatory review record template or storage format. [Ref: §15]

## 7. Completion Criteria

An Inspection is complete when ALL of the following hold:

| ID | Criterion | Source |
|---|---|---|
| **IC-1** | All checklist items in §5 have been addressed (checked, not-applicable, or explicitly deferred with rationale). | Derived from RV-3 [Ref: §15.2] |
| **IC-2** | A review record per §6 has been produced and stored. [Ref: RV-5, §15.2] | §15.2 RV-5 |
| **IC-3** | Findings, if any, have been dispositioned. | Derived from RV-5 [Ref: §15.2] |
| **IC-4** | For Inspections of standard changes (RV-2): the change has been approved by the designated Standard Authority after Inspection. [Ref: GV-3] | §17.2 GV-3 |
| **IC-5** | For fail or conditional-pass dispositions: required rework items have been defined and re-inspection criteria stated. | Derived from RV-5 [Ref: §15.2] |

SDD does not specify whether a single reviewer or multiple reviewers are required for Inspection completion. [Ref: §15]

---

*This checklist is a derived artifact per §11.1. It derives authority from §15.1 and §15.2 and MUST NOT introduce normative rules independent of the SDD.*
