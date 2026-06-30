# Management Review Checklist

> **Authority Class:** Derived
> **SDD Authority:** §15.1, §15.2, §15.3, §17
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the Management Review checklist for the Software Engineering Standard (SES). Management Review is a status and decision review conducted by authority at governance gates. [Ref: §15.1, §17]

## 2. Scope

This checklist applies to Management Reviews conducted under the SES Review Model (§15). Management Review is a status/decision review by the Standard Authority (STK-1) at governance gates. [Ref: §15.1, §17.2]

SDD does not specify the frequency or scheduling of Management Reviews. [Ref: §15.1]

## 3. Normative Rules (RV-1..RV-5)

The following normative rules apply to all review types, including Management Review, and MUST be verified as part of every Management Review. [Ref: §15.2]

| Rule | Statement | Verification |
|---|---|---|
| **RV-1** | Every authoritative artifact MUST pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2] | Confirm the artifact or decision under review has met prerequisite reviews. |
| **RV-2** | Changes to the standard itself MUST undergo Inspection. [Ref: §15.2] | Confirm that changes to the SES have passed Inspection before reaching Management Review. [Ref: GV-3] |
| **RV-3** | Review MUST be against explicit, written criteria (checklists/verification criteria), not reviewer preference. [Ref: §15.2] | Confirm this checklist or another written criteria document is the basis for the review. |
| **RV-4** | Review of work SHOULD be performed by someone other than its sole author where independence adds value. [Ref: §15.2] | Confirm the reviewing authority is distinct from the proposer/originator. |
| **RV-5** | Review outcomes (findings, disposition) MUST be recorded as evidence. [Ref: §15.2] | Confirm a review record artifact exists and will be retained. |

## 4. Review Target (Governance Gates)

Per §15.1 and §17, Management Review SHALL be applied at the following governance gates:

| Gate | Description | Authority |
|---|---|---|
| **Change approval** | Approval of proposed changes to the SES after Inspection. [Ref: GV-3] | Standard Authority (STK-1) [Ref: §17.2 GV-3] |
| **Version release** | Approval of a new standard version. [Ref: VS-1, GV-5] | Standard Authority [Ref: §17.2 GV-5] |
| **Conformance certification** | Recognition that a project satisfies SES requirements. [Ref: §16.5] | Standard Authority |
| **Governance model selection** | Selection among documented governance models. [Ref: §17.3] | Standard Authority |

SDD does not specify the complete set of governance gates requiring Management Review. [Ref: §17]

## 5. Checklist

### 5.1 Pre-Review Readiness

| ID | Item | Source |
|---|---|---|
| MR-P1 | The item under review MUST have passed prerequisite reviews (e.g., Inspection for standard changes per RV-2). [Ref: RV-2, GV-3] | §15.2 RV-2, §17.2 GV-3 |
| MR-P2 | The reviewing authority MUST be the designated Standard Authority (STK-1). [Ref: GV-3] | §17.2 GV-3 |
| MR-P3 | The proposal MUST contain: the problem, the evidence, the proposed change, the impact on existing requirements, and the affected versions. [Ref: GV-2] | §17.2 GV-2 |
| MR-P4 | Reviewers MUST have access to the explicit, written criteria against which the Management Review is conducted. [Ref: §15.2 RV-3] | §15.2 |

### 5.2 Governance Criteria

Per §17.2, the following normative governance rules MUST be verified during Management Review. [Ref: §17.2]

| ID | Item | Source |
|---|---|---|
| MR-G1 | The proposed change MUST NOT be a project-local modification; projects MUST NOT modify the core standard. [Ref: GV-1] | §17.2 GV-1 |
| MR-G2 | The proposal MUST contain all required elements: problem, evidence, proposed change, impact on existing requirements, affected versions. [Ref: GV-2] | §17.2 GV-2 |
| MR-G3 | If the proposal is a change to the standard, it MUST have undergone Inspection before Management Review. [Ref: GV-3, RV-2] | §17.2 GV-3, §15.2 RV-2 |
| MR-G4 | The change MUST be supported by evidence from the approved evidence base (Appendix A) or be explicitly marked UNSUPPORTED. [Ref: GV-4] | §17.2 GV-4 |
| MR-G5 | Every accepted change MUST produce: a version increment (§18 VS-1), a changelog entry (§18 VS-2), and an ADR recording the decision and its rationale. [Ref: GV-5] | §17.2 GV-5 |
| MR-G6 | The standard MUST maintain a single, identifiable current authoritative version; superseded versions are retained for history but are non-governing. [Ref: GV-6] | §17.2 GV-6 |

### 5.3 Evidence and Support

| ID | Item | Source |
|---|---|---|
| MR-E1 | The proposal MUST cite evidence from the approved evidence base (Appendix A) or be marked UNSUPPORTED. [Ref: GV-4, PR-1] | §17.2 GV-4, §7 PR-1 |
| MR-E2 | Unevidenced changes MUST NOT be accepted as normative. [Ref: GV-4] | §17.2 GV-4 |
| MR-E3 | The impact of the change on existing requirements MUST be documented. [Ref: GV-2] | §17.2 GV-2 |

### 5.4 Versioning Criteria

Per §18, the following versioning rules MUST be verified during Management Review of a version release. [Ref: §18]

| ID | Item | Source |
|---|---|---|
| MR-V1 | The release MUST carry a unique semantic version. [Ref: VS-1] | §18 VS-1 |
| MR-V2 | The change MUST be recorded in a changelog stating what changed and why. [Ref: VS-2] | §18 VS-2 |
| MR-V3 | If MAJOR increment: a migration note MUST be included describing what conforming projects must do. [Ref: VS-4] | §18 VS-4 |
| MR-V4 | Backward-incompatible changes MUST NOT be released as MINOR or PATCH. [Ref: VS-5] | §18 VS-5 |
| MR-V5 | A deprecation period SHOULD be defined for rules being removed. [Ref: VS-6] | §18 VS-6 |

### 5.5 Roles and Authority

Per §17.2 GV-7, roles MUST be defined. The following items apply where roles are defined. [Ref: §17.2 GV-7]

| ID | Item | Source |
|---|---|---|
| MR-R1 | Roles MUST be defined (at minimum: Standard Authority, Maintainer, Reviewer, Contributor/Project). [Ref: GV-7] | §17.2 GV-7 |
| MR-R2 | The reviewing authority MUST be the designated Standard Authority. [Ref: GV-3] | §17.2 GV-3 |

SDD does not specify a detailed RACI matrix; detailed role definitions are a Phase-7 deliverable. [Ref: §17.2 GV-7]

### 5.6 Governance Model Selection

Per §17.3, if the Management Review addresses governance model selection, the following apply. [Ref: §17.3]

| ID | Item | Source |
|---|---|---|
| MR-M1 | The governance model selection MUST be justified in context. [Ref: §17.3] | §17.3 |
| MR-M2 | Documented governance models that MUST be compared include: BDFL/single-authority, maintainer-hierarchy (Linux kernel), committee/foundation (Apache, CNCF, IETF). [Ref: §17.3] | §17.3 |

### 5.7 Risk Assessment

| ID | Item | Source |
|---|---|---|
| MR-K1 | Risks associated with the proposed change or decision MUST be identified. [Ref: §21] | §21 |
| MR-K2 | Risk mitigations MUST be documented where risks are identified. | Derived from §21 |

### 5.8 Review/Validation Separation

| ID | Item | Source |
|---|---|---|
| MR-X1 | The Management Review MUST NOT be conflated with validation; review is human/criteria-based examination, validation is objective conformance verification. [Ref: §15.3, PR-8] | §15.3 |

## 6. Recording Requirements (RV-5)

Per RV-5, every Management Review MUST produce a review record containing: [Ref: §15.2]

| Field | Required | Source |
|---|---|---|
| Item or proposal under review | MUST | RV-5 [Ref: §15.2] |
| Review date | MUST | RV-5 [Ref: §15.2] |
| Reviewing authority (Standard Authority) | MUST | GV-3 [Ref: §17.2] |
| Criteria document used (this checklist or other) | MUST | RV-3 [Ref: §15.2] |
| Prerequisite reviews completed | MUST | RV-2 [Ref: §15.2] |
| Evidence cited in proposal | MUST | GV-4 [Ref: §17.2] |
| Impact on existing requirements | MUST | GV-2 [Ref: §17.2] |
| Affected versions | MUST | GV-2 [Ref: §17.2] |
| Decision (approved / rejected / deferred) | MUST | RV-5 [Ref: §15.2] |
| Conditions of approval, if any | MUST (if approved with conditions) | RV-5 [Ref: §15.2] |
| Required version increment | MUST (if change approved) | GV-5 [Ref: §17.2] |
| ADR reference for the decision | MUST (if change approved) | GV-5 [Ref: §17.2] |
| Risks identified | MUST (if applicable) | §21 |

SDD does not specify a mandatory Management Review record template or storage format. [Ref: §15, §17]

## 7. Completion Criteria

A Management Review is complete when ALL of the following hold:

| ID | Criterion | Source |
|---|---|---|
| **MRC-1** | All checklist items in §5 applicable to the review scope have been addressed (checked, not-applicable, or explicitly deferred with rationale). | Derived from RV-3 [Ref: §15.2] |
| **MRC-2** | A review record per §6 has been produced and stored. [Ref: RV-5, §15.2] | §15.2 RV-5 |
| **MRC-3** | A decision (approved / rejected / deferred) has been recorded. [Ref: RV-5] | §15.2 RV-5 |
| **MRC-4** | For approved changes: a version increment, changelog entry, and ADR have been identified or produced. [Ref: GV-5] | §17.2 GV-5 |
| **MRC-5** | For deferred decisions: conditions for re-review have been recorded. | Derived from RV-5 [Ref: §15.2] |
| **MRC-6** | For rejected proposals: the rationale for rejection has been recorded. | Derived from RV-5 [Ref: §15.2] |

SDD does not specify escalation procedures if the Standard Authority is unavailable to conduct Management Review. [Ref: §17]

---

*This checklist is a derived artifact per §11.1. It derives authority from §15.1, §15.2, and §17 and MUST NOT introduce normative rules independent of the SDD.*
