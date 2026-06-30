# Conformance Assertion Template

| Field | Value |
|---|---|
| **Artifact ID** | `[ARTIFACT_ID]` |
| **Artifact Type** | Conformance Assertion |
| **Authority Class** | Authoritative |
| **Owner** | `[OWNER_NAME]` |
| **Version** | `[VERSION]` |
| **Status** | `[STATUS]` |
| **Standard Version** | `[SES_VERSION]` |
| **Created** | `[DATE]` |

---

> **SDD Authority:** This template is derived from the Validation Model (§16.5). [Ref: §16.5]
>
> **Normative Basis:** A conformance assertion is "a recorded, evidenced statement that a project satisfies the applicable SES requirements at a stated standard version." [Ref: §16.5]
> This mechanism makes "the standard governs projects" verifiable rather than aspirational per OBJ-7 and FR-15. [Ref: §3 OBJ-7, §8 FR-15]
> Every conformance assertion MUST conform to: VL-1 (objective pass/fail); VL-4 (verdict cites evidence); VS-3 (names standard version). [Ref: §16.4]

---

## 1. Project Name

[PLACEHOLDER: Name of the project being assessed for conformance to the SES.]

| Field | Value |
|---|---|
| **Project Name** | `[PROJECT_NAME]` |
| **Project ID** | `[PROJECT_ID]` |
| **Repository** | `[REPOSITORY_URL]` |
| **Technology Domain** | `[DOMAIN]` |

---

## 2. Standard Version

> A project's conformance assertion MUST name the standard version it conforms to per VS-3. [Ref: §18, VS-3]

| Field | Value |
|---|---|
| **SES Version** | `[SES_VERSION]` |
| **Version Date** | `[VERSION_DATE]` |
| **Core Only / With Extensions** | `[SCOPE]` |
| **Extension References (if applicable)** | `[EXTENSION_REFS]` |

---

## 3. Assertion Date

| Field | Value |
|---|---|
| **Assertion Date** | `[ASSERTION_DATE]` |
| **Assertion Valid From** | `[VALID_FROM]` |
| **Assertion Valid Until** | `[EXPIRATION_DATE]` |
| **Re-assessment Trigger** | `[TRIGGER]` |

---

## 4. Asserting Party

> The asserting party MUST be identifiable and accountable per §17 (Governance Model). [Ref: §17]

| Field | Value |
|---|---|
| **Asserting Party** | `[ASSERTING_PARTY]` |
| **Role** | `[ROLE]` |
| **Organization** | `[ORGANIZATION]` |
| **Contact** | `[CONTACT]` |
| **Authorization Basis** | `[AUTH_BASIS]` |

---

## 5. Scope of Conformance

> Define which parts of the SES are claimed to be satisfied. Extensions MUST declare which standard version and core rules they extend per EX-5. [Ref: §19, EX-5]

| Scope Item | Included? | Notes |
|---|---|---|
| **Engineering Lifecycle (§12)** | [ ] | `[NOTES]` |
| **Stage Model (§13)** | [ ] | `[NOTES]` |
| **Knowledge Model (§14)** | [ ] | `[NOTES]` |
| **Review Model (§15)** | [ ] | `[NOTES]` |
| **Validation Model (§16)** | [ ] | `[NOTES]` |
| **Governance Model (§17)** | [ ] | `[NOTES]` |
| **Versioning Strategy (§18)** | [ ] | `[NOTES]` |
| **Extension Policy (§19)** | [ ] | `[NOTES]` |
| **Artifact Architecture (§11)** | [ ] | `[NOTES]` |
| **Engineering Mission Model (§32)** | [ ] | `[NOTES]` |
| **Engineering State Model (§33)** | [ ] | `[NOTES]` |
| **Engineering Operation Model (§34)** | [ ] | `[NOTES]` |
| **Engineering Decision Model (§35)** | [ ] | `[NOTES]` |
| **Engineering Impact Analysis (§36)** | [ ] | `[NOTES]` |
| **Engineering Integrity Rules (§40)** | [ ] | `[NOTES]` |
| **Repository Readiness (§41)** | [ ] | `[NOTES]` |

---

## 6. Requirements Satisfied

> Each requirement class MUST have a defined verification method per VL-2. [Ref: §16.4, VL-2]
> Conformance MUST be expressed as objective pass/fail against stated criteria per VL-1. [Ref: §16.4, VL-1]

| Requirement Class | SDD Reference | Verification Method | Status | Evidence |
|---|---|---|---|---|
| `[REQ-1]` | `[REF]` | Inspection / Analysis / Demonstration / Test | Pass / Fail | `[EVIDENCE]` |
| `[REQ-2]` | `[REF]` | Inspection / Analysis / Demonstration / Test | Pass / Fail | `[EVIDENCE]` |
| `[REQ-3]` | `[REF]` | Inspection / Analysis / Demonstration / Test | Pass / Fail | `[EVIDENCE]` |
| `[REQ-4]` | `[REF]` | Inspection / Analysis / Demonstration / Test | Pass / Fail | `[EVIDENCE]` |
| `[REQ-5]` | `[REF]` | Inspection / Analysis / Demonstration / Test | Pass / Fail | `[EVIDENCE]` |

---

## 7. Evidence Summary

> A conformance verdict MUST cite the evidence on which it rests per VL-4. [Ref: §16.4, VL-4]
> Validation evidence MUST be recorded and reproducible per VL-3. [Ref: §16.4, VL-3]

| Evidence ID | Type | Description | Location | Confidence Level |
|---|---|---|---|---|
| `[EV-1]` | `[TYPE]` | `[DESCRIPTION]` | `[LOCATION]` | A / B / C / D / E |
| `[EV-2]` | `[TYPE]` | `[DESCRIPTION]` | `[LOCATION]` | A / B / C / D / E |
| `[EV-3]` | `[TYPE]` | `[DESCRIPTION]` | `[LOCATION]` | A / B / C / D / E |

> **Confidence Levels (§26.2):** A = Observed at runtime; B = Confirmed by implementation; C = Confirmed by documentation; D = Derived from multiple sources; E = Engineering hypothesis. [Ref: §26.2]

---

## 8. Verdict

> Conformance MUST be expressed as objective pass/fail against stated criteria per VL-1. [Ref: §16.4, VL-1]

| Field | Value |
|---|---|
| **Overall Verdict** | Pass / Fail / Partial / Expired |
| **Conformance Statement** | `[STATEMENT]` |
| **Conditions or Limitations** | `[CONDITIONS]` |
| **Non-conformant Items (if any)** | `[NON_CONFORMANT_ITEMS]` |
| **Risk Assessment** | `[RISK_ASSESSMENT]` |

---

## 9. Review Reference

> The conformance assertion itself SHOULD be subject to review per §15. [Ref: §15]

| Field | Value |
|---|---|
| **Review Record ID** | `[REVIEW_RECORD_ID]` |
| **Review Type** | Inspection / Technical Review / Audit |
| **Review Date** | `[DATE]` |
| **Reviewer(s)** | `[REVIEWERS]` |
| **Review Verdict** | Pass / Fail / Conditional |

---

## 10. Expiration Date

| Field | Value |
|---|---|
| **Assertion Expires** | `[EXPIRATION_DATE]` |
| **Re-assessment Required By** | `[REASSESSMENT_DATE]` |
| **Expiration Trigger(s)** | `[TRIGGERS]` |
| **Post-Expiration Status** | `[POST_EXPIRY_STATUS]` |

---

## 11. Traceability

| Trace Link | Reference |
|---|---|
| **Project Repository** | `[REPO_URL]` |
| **Conformance Audit** | `[AUDIT_ID]` |
| **Review Record** | `[REVIEW_ID]` |
| **Governance Decision** | `[DECISION_ID]` |
| **Related Conformance Assertions** | `[RELATED_ASSERTIONS]` |
| **Repository Location** | `[FILE_PATH]` |

---

## Integrity Rules Assessment (§40)

> Violation of any INT rule renders the affected work non-conformant per §40.2. [Ref: §40.2]

| Rule ID | Statement | Compliant? |
|---|---|---|
| **INT-1** | No undocumented implementation. [Ref: §40.1] | [ ] |
| **INT-2** | No undocumented decision. [Ref: §40.1] | [ ] |
| **INT-3** | No undocumented dependency. [Ref: §40.1] | [ ] |
| **INT-4** | No undocumented API. [Ref: §40.1] | [ ] |
| **INT-5** | No undocumented database object. [Ref: §40.1] | [ ] |
| **INT-6** | No undocumented configuration. [Ref: §40.1] | [ ] |
| **INT-7** | No undocumented workflow. [Ref: §40.1] | [ ] |
| **INT-8** | No undocumented security rule. [Ref: §40.1] | [ ] |
| **INT-9** | No undocumented assumption. [Ref: §40.1] | [ ] |
| **INT-10** | No undocumented evidence. [Ref: §40.1] | [ ] |

---

> **Placeholder count:** 24 distinct `[PLACEHOLDER]` fields.
