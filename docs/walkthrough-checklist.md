# Walkthrough Checklist

> **Authority Class:** Derived
> **SDD Authority:** §15.1, §15.2, §15.3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the Walkthrough review checklist for the Software Engineering Standard (SES). Walkthrough is an author-led, educational review type providing early feedback, applied at early-stage understanding and recovery activities. [Ref: §15.1]

## 2. Scope

This checklist applies to Walkthroughs conducted under the SES Review Model (§15). Walkthrough is an author-led, educational, early-feedback activity distinct from the formal defect detection of Inspection. [Ref: §15.1]

SDD does not specify the minimum or maximum number of participants for a Walkthrough. [Ref: §15.1]

## 3. Normative Rules (RV-1..RV-5)

The following normative rules apply to all review types, including Walkthrough, and MUST be verified as part of every Walkthrough. [Ref: §15.2]

| Rule | Statement | Verification |
|---|---|---|
| **RV-1** | Every authoritative artifact MUST pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2] | Confirm the artifact under review has not been previously declared effective without review. Note: Walkthrough alone may not satisfy RV-1 for authoritative artifacts that require a more rigorous review type. |
| **RV-2** | Changes to the standard itself MUST undergo Inspection. [Ref: §15.2] | Confirm the artifact is not a change to the SES (which would require Inspection, not Walkthrough). |
| **RV-3** | Review MUST be against explicit, written criteria (checklists/verification criteria), not reviewer preference. [Ref: §15.2] | Confirm this checklist or another written criteria document is the basis for the walkthrough. |
| **RV-4** | Review of work SHOULD be performed by someone other than its sole author where independence adds value. [Ref: §15.2] | Confirm reviewer independence from the artifact's sole authorship. Note: Walkthrough is author-led; independence applies to other participants. |
| **RV-5** | Review outcomes (findings, disposition) MUST be recorded as evidence. [Ref: §15.2] | Confirm a review record artifact exists and will be retained. |

## 4. Review Target (Early-Stage Understanding and Recovery)

Per §15.1, Walkthrough SHALL be applied in the following contexts:

| Context | Position in Lifecycle | Rationale |
|---|---|---|
| **Early-stage understanding** | Discovery / Understanding phases [Ref: §12.2] | Author-led review to build shared understanding of an unknown system. [Ref: §15.1, §25] |
| **Recovery** | Reverse Engineering / Reconstruction [Ref: §12.2, §30] | Author-led review to validate recovered understanding before it is recorded as authoritative fact. [Ref: §15.1, §30] |

SDD does not specify additional Walkthrough contexts beyond early-stage understanding and recovery. [Ref: §15.1]

## 5. Checklist

### 5.1 Pre-Walkthrough Readiness

| ID | Item | Source |
|---|---|---|
| WT-P1 | The artifact or material under review MUST be in a presentable state sufficient for educational walkthrough. | SDD does not specify pre-walkthrough readiness conditions. [Ref: §15] |
| WT-P2 | The author/leader MUST be present to guide the walkthrough. | Derived from "author-led" [Ref: §15.1] |
| WT-P3 | Participants MUST have access to the explicit, written criteria against which the Walkthrough is conducted. [Ref: §15.2 RV-3] | §15.2 |
| WT-P4 | The objective of the Walkthrough MUST be stated (e.g., build understanding, validate recovery, early feedback on a design). | Derived from "early feedback" [Ref: §15.1] |

### 5.2 Author-Led Review Criteria

Per §15.1, Walkthrough is "author-led, educational, early feedback." The following checklist items operationalize these properties. [Ref: §15.1]

| ID | Item | Source |
|---|---|---|
| WT-A1 | The author MUST lead the walkthrough, presenting the material and explaining its rationale. | Derived from "author-led" [Ref: §15.1] |
| WT-A2 | The walkthrough MUST have an educational objective: participants SHOULD gain understanding of the material. | Derived from "educational" [Ref: §15.1] |
| WT-A3 | Feedback obtained MUST be early in the lifecycle: the artifact under walkthrough SHOULD NOT yet be declared authoritative or effective. | Derived from "early feedback" [Ref: §15.1] |

### 5.3 Discovery and Recovery Alignment

When the Walkthrough is conducted during Discovery (§25) or Recovery (§30), the following additional items apply. [Ref: §15.1]

| ID | Item | Source |
|---|---|---|
| WT-D1 | Observations presented during the walkthrough MUST be distinguished from verified facts. [Ref: KN-1, KN-3] | §14.3 KN-1, KN-3 |
| WT-D2 | Hypotheses about the system MUST be explicitly marked as hypotheses. [Ref: KN-3] | §14.3 KN-3 |
| WT-D3 | Recovered abstractions MUST be linked to the source artifacts from which they were derived. [Ref: REV-2, §28] | §30.3 REV-2, §28 |
| WT-D4 | Disagreements or uncertainties MUST be recorded, not silently resolved. [Ref: DSC-3] | §25.4 DSC-3 |
| WT-D5 | Walkthrough findings that result in recorded facts MUST carry provenance. [Ref: KN-1, PR-5] | §14.3 KN-1 |

### 5.4 Artifact Authority

| ID | Item | Source |
|---|---|---|
| WT-M1 | Material under Walkthrough MAY be non-authoritative (observed facts, hypotheses, draft understanding). | Derived from "early-stage" positioning [Ref: §15.1] |
| WT-M2 | If the Walkthrough material is intended to become authoritative, the artifact MUST carry mandatory metadata per §11.2. [Ref: §11.2] | §11.2 |
| WT-M3 | If the Walkthrough material is intended to become authoritative, it MUST pass a subsequent review of an appropriate type (Inspection or Technical Review) before becoming effective per RV-1. [Ref: RV-1] | §15.2 RV-1 |

### 5.5 Evidence and Provenance

| ID | Item | Source |
|---|---|---|
| WT-E1 | Any fact recorded as a result of the Walkthrough MUST carry provenance. [Ref: KN-1] | §14.3 KN-1 |
| WT-E2 | Confidence levels assigned to walkthrough-derived facts MUST reflect the evidence strength, not assertion. [Ref: EVC-5] | §26.4 EVC-5 |

### 5.6 Review/Validation Separation

| ID | Item | Source |
|---|---|---|
| WT-V1 | The Walkthrough MUST NOT be conflated with validation; review is human/criteria-based examination, validation is objective conformance verification. [Ref: §15.3, PR-8] | §15.3 |
| WT-V2 | The Walkthrough MUST NOT be used as the sole review for high-risk artifacts requiring Inspection. [Ref: §15.1, RV-2] | §15.1, §15.2 RV-2 |

## 6. Recording Requirements (RV-5)

Per RV-5, every Walkthrough MUST produce a review record containing: [Ref: §15.2]

| Field | Required | Source |
|---|---|---|
| Material identifier or description | MUST | RV-5 [Ref: §15.2] |
| Walkthrough date | MUST | RV-5 [Ref: §15.2] |
| Author/leader | MUST | Derived from "author-led" [Ref: §15.1] |
| Participants | MUST | RV-5 [Ref: §15.2] |
| Objective of the walkthrough | MUST | Derived from "educational, early feedback" [Ref: §15.1] |
| Criteria document used (this checklist or other) | MUST | RV-3 [Ref: §15.2] |
| Findings, questions, and feedback | MUST | RV-5 [Ref: §15.2] |
| Action items resulting from feedback | MUST (if applicable) | RV-5 [Ref: §15.2] |
| Follow-up review type required, if any | MUST (if artifact to become authoritative) | RV-1 [Ref: §15.2] |

SDD does not specify a mandatory walkthrough record template or storage format. [Ref: §15]

## 7. Completion Criteria

A Walkthrough is complete when ALL of the following hold:

| ID | Criterion | Source |
|---|---|---|
| **WTC-1** | All applicable checklist items in §5 have been addressed (checked, not-applicable, or explicitly deferred with rationale). | Derived from RV-3 [Ref: §15.2] |
| **WTC-2** | A review record per §6 has been produced and stored. [Ref: RV-5, §15.2] | §15.2 RV-5 |
| **WTC-3** | Feedback and action items, if any, have been recorded. | Derived from RV-5 [Ref: §15.2] |
| **WTC-4** | If the artifact is intended to become authoritative, the required follow-up review type has been identified and scheduled. [Ref: RV-1] | §15.2 RV-1 |
| **WTC-5** | If the walkthrough occurred during Discovery or Recovery, observations have been distinguished from verified facts per KN-3. [Ref: KN-3] | §14.3 KN-3 |

SDD does not specify time limits for Walkthrough duration or time-to-completion. [Ref: §15]

---

*This checklist is a derived artifact per §11.1. It derives authority from §15.1 and §15.2 and MUST NOT introduce normative rules independent of the SDD.*
