# Technical Review Checklist

> **Authority Class:** Derived
> **SDD Authority:** §15.1, §15.2, §15.3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the Technical Review checklist for the Software Engineering Standard (SES). Technical Review evaluates the fitness for purpose of design documents and plans by qualified reviewers. [Ref: §15.1]

## 2. Scope

This checklist applies to Technical Reviews conducted under the SES Review Model (§15). Technical Review is a criteria-based examination to evaluate whether an artifact is fit for its intended engineering purpose. [Ref: §15.1]

SDD does not specify a formal minimum qualification for "qualified reviewers." [Ref: §15.1]

## 3. Normative Rules (RV-1..RV-5)

The following normative rules apply to all review types, including Technical Review, and MUST be verified as part of every Technical Review. [Ref: §15.2]

| Rule | Statement | Verification |
|---|---|---|
| **RV-1** | Every authoritative artifact MUST pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2] | Confirm the artifact under review has not been previously declared effective without review. |
| **RV-2** | Changes to the standard itself MUST undergo Inspection. [Ref: §15.2] | Confirm the artifact is not a change to the SES (which would require Inspection, not Technical Review). |
| **RV-3** | Review MUST be against explicit, written criteria (checklists/verification criteria), not reviewer preference. [Ref: §15.2] | Confirm this checklist or another written criteria document is the basis for the review. |
| **RV-4** | Review of work SHOULD be performed by someone other than its sole author where independence adds value. [Ref: §15.2] | Confirm reviewer independence from the artifact's sole authorship. |
| **RV-5** | Review outcomes (findings, disposition) MUST be recorded as evidence. [Ref: §15.2] | Confirm a review record artifact exists and will be retained. |

## 4. Review Target (Design Documents and Plans)

Per §15.1, Technical Review SHALL be applied to evaluate fitness for purpose of the following artifact categories:

| Category | Authority Class | Rationale |
|---|---|---|
| **Design documents** | Authoritative | Design documents govern implementation direction; fitness for purpose must be verified before implementation. [Ref: §15.1] |
| **Plans** | Authoritative | Plans sequence and bound engineering work; their feasibility and coverage must be verified. [Ref: §15.1] |

SDD does not specify a complete catalog of design document and plan artifact types. [Ref: §11.4]

## 5. Checklist

### 5.1 Pre-Review Readiness

| ID | Item | Source |
|---|---|---|
| TR-P1 | The artifact under review MUST be in a stable, readable state. | SDD does not specify pre-review readiness conditions. [Ref: §15] |
| TR-P2 | The artifact MUST carry mandatory artifact metadata per §11.2: unique identifier, authority class, owner, version, status. [Ref: §11.2] | §11.2 |
| TR-P3 | Reviewers MUST have access to the explicit, written criteria against which the Technical Review is conducted. [Ref: §15.2 RV-3] | §15.2 |
| TR-P4 | The artifact MUST define its intended purpose and scope. | Derived from "fitness for purpose" definition [Ref: §15.1] |

### 5.2 Artifact Authority and Metadata

| ID | Item | Source |
|---|---|---|
| TR-A1 | The artifact MUST declare its authority class (authoritative / derived / generated). [Ref: §11.1] | §11.1 |
| TR-A2 | The artifact MUST carry a version identifier consistent with the SES versioning strategy (§18). [Ref: §11.2] | §11.2, §18 |
| TR-A3 | The artifact MUST declare its owner. [Ref: §11.2] | §11.2 |

### 5.3 Fitness for Purpose (Core Technical Review Criteria)

Per §15.1, the purpose of Technical Review is to "evaluate fitness for purpose by qualified reviewers." The following checklist items operationalize this requirement against SES rules. [Ref: §15.1]

| ID | Item | Source |
|---|---|---|
| TR-F1 | The artifact MUST satisfy its stated objective; the reviewer MUST confirm the artifact achieves its declared purpose. | Derived from "fitness for purpose" [Ref: §15.1] |
| TR-F2 | The artifact MUST be consistent with the SES Engineering Principles (§7). | §7 |
| TR-F3 | The artifact MUST NOT contradict any normative rule in the SES. [Ref: NFR-11] | §9 NFR-11 |
| TR-F4 | The artifact MUST use RFC 2119 keywords (MUST, MUST NOT, SHALL, SHOULD, MAY) consistently per §46 and NFR-4. [Ref: §46, NFR-4] | §46, §9 NFR-4 |
| TR-F5 | The artifact MUST NOT name or require a specific commercial product, programming language, framework, or AI model unless it is an extension per §19. [Ref: FR-16, PR-3] | §8 FR-16, §7 PR-3 |

### 5.4 Evidence and Provenance

| ID | Item | Source |
|---|---|---|
| TR-E1 | Every normative rule in the artifact MUST carry an evidence reference or an explicit UNSUPPORTED marker. [Ref: FR-11, PR-1] | §8 FR-11 |
| TR-E2 | If the artifact contains recorded facts, each MUST carry provenance linking it to source evidence. [Ref: KN-1] | §14.3 KN-1 |
| TR-E3 | Hypotheses in the artifact MUST be marked as hypotheses and MUST NOT be presented as verified facts. [Ref: KN-3] | §14.3 KN-3 |

### 5.5 Traceability

| ID | Item | Source |
|---|---|---|
| TR-T1 | If the artifact contains requirements, each MUST be traceable forward to verification and backward to principle/objective. [Ref: FR-14, PR-5] | §8 FR-14, §7 PR-5 |
| TR-T2 | The artifact MUST cite the SDD section(s) from which it derives authority. [Ref: RA-5, §10.4] | §10.4 RA-5 |

### 5.6 Stage-Gate Alignment

| ID | Item | Source |
|---|---|---|
| TR-S1 | If the artifact is a stage output, the artifact MUST be classified per the Artifact Authority Model (§11). [Ref: SG-2] | §13.3 SG-2 |
| TR-S2 | If the artifact gates a stage, the reviewer MUST confirm the stage's exit criteria are addressed by the artifact. [Ref: SG-1] | §13.3 SG-1 |

### 5.7 Review/Validation Separation

| ID | Item | Source |
|---|---|---|
| TR-V1 | The Technical Review MUST NOT be conflated with validation; review is human/criteria-based examination, validation is objective conformance verification. [Ref: §15.3, PR-8] | §15.3 |

## 6. Recording Requirements (RV-5)

Per RV-5, every Technical Review MUST produce a review record containing: [Ref: §15.2]

| Field | Required | Source |
|---|---|---|
| Artifact identifier | MUST | §11.2 |
| Artifact version reviewed | MUST | §11.2 |
| Review date | MUST | RV-5 [Ref: §15.2] |
| Reviewer(s) | MUST | RV-5 [Ref: §15.2] |
| Criteria document used (this checklist or other) | MUST | RV-3 [Ref: §15.2] |
| Findings (defects, questions, observations) | MUST | RV-5 [Ref: §15.2] |
| Fitness-for-purpose verdict (fit / not fit / conditionally fit) | MUST | Derived from §15.1 |
| Required rework items, if any | MUST (if not fit or conditionally fit) | RV-5 [Ref: §15.2] |
| Evidence of reviewer independence (RV-4) | SHOULD | RV-4 [Ref: §15.2] |
| Reviewer qualifications | SHOULD | Derived from "qualified reviewers" [Ref: §15.1] |

SDD does not specify a mandatory review record template or storage format. [Ref: §15]

## 7. Completion Criteria

A Technical Review is complete when ALL of the following hold:

| ID | Criterion | Source |
|---|---|---|
| **TRC-1** | All checklist items in §5 have been addressed (checked, not-applicable, or explicitly deferred with rationale). | Derived from RV-3 [Ref: §15.2] |
| **TRC-2** | A review record per §6 has been produced and stored. [Ref: RV-5, §15.2] | §15.2 RV-5 |
| **TRC-3** | Findings, if any, have been dispositioned. | Derived from RV-5 [Ref: §15.2] |
| **TRC-4** | For not-fit or conditionally-fit verdicts: required rework items have been defined and re-review criteria stated. | Derived from RV-5 [Ref: §15.2] |
| **TRC-5** | The reviewer(s) have confirmed their independence from sole authorship per RV-4, or recorded the rationale if independence was not achievable. [Ref: RV-4] | §15.2 RV-4 |

SDD does not specify whether a single reviewer or multiple reviewers are required for Technical Review completion. [Ref: §15]

---

*This checklist is a derived artifact per §11.1. It derives authority from §15.1 and §15.2 and MUST NOT introduce normative rules independent of the SDD.*
